#!/bin/bash

mkdir -p pokemon_data

POKEMON_LIST=(bulbasaur ivysaur venusaur charmander charmeleon)
MAX_RETRIES=3

for POKEMON in "${POKEMON_LIST[@]}"; do
    echo "Fetching data for $POKEMON..."
    SUCCESS=false
    for ((i=1; i<=MAX_RETRIES; i++)); do
        if curl -sS "https://pokeapi.co/api/v2/pokemon/${POKEMON}" -o "pokemon_data/${POKEMON}.json"; then
            echo "Saved data to pokemon_data/${POKEMON}.json ✅"
            SUCCESS=true
            break
        else
            echo "Attempt $i failed for $POKEMON..."
            sleep 1
        fi
    done
    if [ "$SUCCESS" = false ]; then
        echo "Error: Failed to fetch data for ${POKEMON} after $MAX_RETRIES attempts." >> error_log.txt
    fi
    # Delay between requests
    sleep 1
done
