#!/bin/bash

#Create directories
mkdir -p circos/conf circos/data

#Prepare karyotype
cp example_karyotype.txt circos/conf/karyotype.txt

# Generate karyotype colors
if [ -f karyotype-colors.py ]; then
    python karyotype-colors.py $(grep -c '^chr\s' circos/conf/karyotype.txt) \
        > circos/conf/karyotype-colors.conf
else
    echo "Warning: karyotype-colors.py not found. Using default colors."
    touch circos/conf/karyotype-colors.conf
fi

#Copy configuration files
cp configs/circos.conf   circos/conf/
cp configs/ticks.conf    circos/conf/
cp configs/ideogram.conf circos/conf/
cp configs/data.conf     circos/conf/
cp configs/links.conf    circos/conf/

#Copy data files
cp data/data-0.txt circos/data/
cp data/data-1.txt circos/data/
cp data/data-2.txt circos/data/
 (Add more as needed)

#Run Circos
circos -conf circos/conf/circos.conf -noparanoid
echo "Successfully"
