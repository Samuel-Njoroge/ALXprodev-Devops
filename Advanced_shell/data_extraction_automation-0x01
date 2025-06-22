#!/bin/bash

# Extracting the data using jq
name=$(jq -r '.name' data.json | sed 's/^\(.\)/\U\1/')
height=$(jq -r '.height' data.json)    # in decimeters
weight=$(jq -r '.weight' data.json)    # in hectograms
pokemon_type=$(jq -r '.types[0].type.name' data.json | sed 's/^\(.\)/\U\1/')

# Converting units
height_in_meters=$(awk "BEGIN {printf \"%.1f\", $height/10}")
weight_in_kg=$(awk "BEGIN {printf \"%.1f\", $weight/10}")

# Final Output
echo "$name is of type $pokemon_type, weighs ${weight_in_kg}kg, and is ${height_in_meters}m tall."
