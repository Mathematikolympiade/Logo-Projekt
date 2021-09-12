# CIPS
**C**inderella - **I**ntergeo - Geo<b>P</b>roof<b>S</b>cheme

CIPS is a Java application for conversion
[Cinderella](https://www.cinderella.de) and
[GeoProofSchemes](https://symbolicdata.github.io/Geo) format to
[Intergeo](http://i2geo.net/) format.  CIPS also offers a simple visualization
of the above formats by means of [JSXGraph](https://jsxgraph.org) (for more
details see [*cips.pdf*](cips.pdf)).

## Build CIPS
Prerequisites: Java 1.8, Maven

```
mvn clean install
```

## Usage
```
java -jar cips.jar <mode (optional)> <input file> <output file (optional)> -p [default parameter file]
java -jar cips.jar -c2i <cinderella file path> <intergeo file path>
java -jar cips.jar -g2i <geoproofscheme file> <intergeo file> -p [default parameter file]
java -jar cips.jar -vc  <cinderella file> <visualization file>
java -jar cips.jar -vi  <intergeo file> <visualization file>
java -jar cips.jar -vg  <geoproofscheme file> <visualization file> -p [default parameter file]
example:
java -jar cips.jar -vg testdata/Chou.28_1.xml jsx_Chou_test.html

 -c2i                   cinderella to intergeo
 -g2i                   geoproofscheme to intergeo
 -h,--help              print this message
 -i,--input <arg>       input file path
 -o,--output <arg>      output file path
 -p,--parameter <arg>   default parameter file path
 -vc                    cinderella visualisation with jsxgraph
 -vg                    geoproofscheme visualisation with jsxgraph
 -vi                    intergeo visualisation with jsxgraph
```

## Examples

* Test data found in the folder [testdata](testdata)
* Multimode GeoProofScheme: conversion to Intergeo format & jsxGraph visualisation
(automatically sets output and parameter file; in the source directory)
```
java -jar cips.jar geoproofscheme_test.xml
```
* Visualize GeoProofScheme format
```
java -jar cips.jar -vg geoproofscheme_test.xml geoproofscheme_test.html -p defaultparameters.txt
```

## Team

* Kevin Marco Shrestha (PL) - ks12dyle@studserv.uni-leipzig.de
* Duong Trung Duong - bss13ard@studserv.uni-leipzig.de
* Akber Sarchaddi
* Johannes Michael - jm85copi@studserv.uni-leipzig.de
