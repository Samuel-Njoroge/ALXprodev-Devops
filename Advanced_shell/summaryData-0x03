#!/bin/bash
# This script generates a CSV report of Pokémon data and calculates averages.

REPORT_FILE="pokemon_report.csv"
POKEMON_DIR="pokemon_data"

# Create or overwrite the report file
echo "Name,Height (m),Weight (kg)" > $REPORT_FILE

# Loop through JSON files
for FILE in ${POKEMON_DIR}/*.json; do
    NAME=$(jq -r '.name' "$FILE" | sed 's/^\(.\)/\U\1/')
    HEIGHT=$(jq -r '.height' "$FILE")
    WEIGHT=$(jq -r '.weight' "$FILE")
    HEIGHT_M=$(awk "BEGIN {printf \"%.1f\", $HEIGHT/10}")
    WEIGHT_KG=$(awk "BEGIN {printf \"%.1f\", $WEIGHT/10}")
    echo "$NAME,$HEIGHT_M,$WEIGHT_KG" >> $REPORT_FILE
done

echo "CSV Report generated at: $REPORT_FILE"

echo
cat $REPORT_FILE

echo
# Calculate averages using awk
awk -F',' 'NR>1 {h+=$2; w+=$3; cnt++} END {printf "Average Height: %.2f m\nAverage Weight: %.2f kg\n", h/cnt, w/cnt}' $REPORT_FILE