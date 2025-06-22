#!/bin/bash

# Define the URL and output files
URL="https://pokeapi.co/api/v2/pokemon/pikachu"
OUTPUT_FILE="data.json"
ERROR_FILE="errors.txt"

# Make the API request
curl -sS "$URL" -o "$OUTPUT_FILE"

# Check if curl succeeded
if [ $? -ne 0 ]; then
    echo "Error: Failed to fetch data from $URL" >> "$ERROR_FILE"
    exit 1
fi

# Validate if the output is non-empty and valid JSON 
if [ ! -s "$OUTPUT_FILE" ]; then
    echo "Error: Empty response received from $URL" >> "$ERROR_FILE"
    exit 1
fi

# Validate JSON 
if ! jq empty "$OUTPUT_FILE" 2>/dev/null; then
    echo "Error: Invalid JSON received from $URL" >> "$ERROR_FILE"
    exit 1
fi
