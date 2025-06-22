#!/bin/bash

mkdir -p pokemon_data

POKEMON_LIST=(bulbasaur ivysaur venusaur charmander charmeleon)
MAX_RETRIES=3

fetch_data() {
    local POKEMON=$1
    for ((i=1; i<=MAX_RETRIES; i++)); do
        if curl -sS "https://pokeapi.co/api/v2/pokemon/${POKEMON}" -o "pokemon_data/${POKEMON}.json"; then
            echo "Saved data to pokemon_data/${POKEMON}.json ✅"
            return 0
        else
            echo "Attempt $i failed for $POKEMON..."
            sleep 1
        fi
    done
    echo "Error: Failed to fetch data for ${POKEMON} after $MAX_RETRIES attempts." >> error_log.txt
    return 1
}

# Launch jobs in parallel
for POKEMON in "${POKEMON_LIST[@]}"; do
    echo "Fetching data for $POKEMON..."
    fetch_data $POKEMON &
done

# Wait for all jobs to complete
wait
echo "All downloads completed."
