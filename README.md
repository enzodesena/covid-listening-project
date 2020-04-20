# Sonifying COVID-19 genetic mutations over time

This project aims to turn the genetic mutations of COVID-19 into music. The main objective of the project is to satisfy a personal curiosity and explore the artistic dimension. It is also hoped that **sonifying the mutations could highlight patterns that would not be picked up otherwise**. 

The genome is formed by a long sequence of 4 types of nucleotides: adenine (A), guanine (G), cytosine (c), and uracil (U). This sequence is used to synthesise specific proteins such as the "Spike protein", which gives COVID-19 its crown-like appearance. A mutation happens when a nucleotide is changed, inserted or deleted in the sequence. 

The current sonification methodology associates notes' timing to the position of the mutation within the DNA and pitch to the type of nucleotide mutation (e.g. G->A, or C->U etc). This means that the position of the mutation results in different rhythmic placement, and the type of nucleotide mutation results in different melodies, **giving each genome its own musical signature**. Furthemore, **repeating musical patterns mean that a mutation has persisted over time**. 

Each mutation is associated here to a musical note, giving each genome its own musical signature. The position in the sequence dictates timing and the type of mutation (e.g. adenine to guanine) dictates the pitch. Mutations near the beginning of the sequence are reproduced to your left and later ones to your right. Note that although it may seem like the number of mutations is large, COVID-19 is actually considered a relatively stable virus. 


## Data gathering

The project uses the database of the National Center for Biotechnology Information (NCBI), which is being updated every day with new COVID-19 sequences coming from research centres across the world. The website is available here: [NCBI Covid-19 page](https://www.ncbi.nlm.nih.gov/genbank/sars-cov-2-seqs/)

The data is parsed and downloaded using the [covid-genome-matlab-parser](https://github.com/enzodesena/covid-genome-matlab-parser). 

## How the comparison is run

Please see below the details of the procedure to generate the sound:

* The genomic comparison is run on the basis of the nucleotide sequences (in GACU symbols).
* In order to reduce the amount of data (currently over 700 genomes), only the first measurement of a day is considered; this currently reduces the number of genomes to 74.
* The comparison of genome pairs is carried out using the Needleman-Wunsch global alignment algorithm [1], which allows to identify the genetic mutations.
* The mutations are considered starting from the beginning of the first protein (NSP1), i.e. at nucleotide n. 266 of the NCBI accession MT019529. Mismatches in the last 100 bases are also ignored (for reference, the RNA of COVID-19 is about 30k bases long).
* The nucleotide mutations are translated into notes using the table below; a constant value is added to all of them; the `-` sign indicates an insertion or a deletion; all other types of mutations are ignored.

| Old basis  | New basis | Midi note | Note | 
| ------------- | ------------- |------------- |------------- |
| C | - | 47 |B2|
| U | - | 48 |C3|
| A | - | 49 |C♯3/D♭3|
| G  |  A | 51 | D♯3/E♭3|
| G  |  U | 52 |E3|
| G  |  C | 53 |F3|
| A  |  G | 54 |F♯3/G♭3|
| A  |  U | 55 |G3|
| A  |  C | 56 |G♯3/A♭3|
| U  |  G | 57 |A3|
| U  |  A | 58 |A♯3/B♭3|
| U  |  C | 59 |B3|
| C  |  G | 60 |C4|
| C  |  A | 61 |C♯4/D♭4|
| C  |  U | 62 |D4|
| - | G | 63 |D♯4/E♭4|
| - | A | 64 |E4|
| - | U | 65 |F4|
| - | C | 66 |F♯4/G♭4|
| G | - | 50 |D3|

* The mutations are then organised in 8 groups according to the table below. 

|Protein name|Protein index|Group index|Instrument type|Reproduction Angle|
| ------------- | ------------- |------------- |------------- |------------- |
|NSP1|1|1|Cello|-45°|
|NSP2|2|1|Cello|-45°|
|NSP3|3|2|Cello|-45°|
|NSP4|4|3|Cello|-30°|
|NSP5|5|3|Cello|-15°|
|NSP6|6|3|Cello|-15°|
|NSP7|7|3|Cello|-15°|
|NSP8|8|3|Cello|-15°|
|NSP9|9|4|Cello|0°|
|NSP10|10|4|Cello|0°|
|NSP12|11|4|Cello|0°|
|NSP13|12|5|Cello|+15°|
|NSP14|13|5|Cello|+15°|
|NSP15|14|5|Cello|+15°|
|NSP16|15|5|Cello|+15°|
|S|16|6|Double base|+30°|
|ORF3a|17|7|Violin|+45°|
|E|18|7|Violin|+45°|
|M|19|7|Violin|+45°|
|ORF6|20|7|Violin|+45°|
|ORF7a|21|7|Violin|+45°|
|ORF8|22|7|Violin|+45°|
|N|23|7|Violin|+45°|
|ORF10|24|7|Violin|+45°|
|Non-coding DNA|-|8|Violin|+45°|

* In order to facilitate spatial discrimination, each group is rendered in a different direction, as indicated in the table above. This specific separation corresponds to the actual lenght of each protein. In other words, this results in a similar experience you'd have if the RNA was actually rolled out around you and each mutation would reproduce a sound from a corresponding direction. This means that **not only one can identify the position of the mutation by using the time delay, but also the perceived position of the sound in space**, with mutations closer to the beginning of the sequence appearing to your left, while later ones appearing to your right. The specific spatialisation technique used here is Perceptual Soundfield Reconstruction (PSR) [2,3,4]. 

* In order to increase presence, each source is rendered with reverberation using Scattering Delay Networks (SDN) [2,5]; the simulated room is rectangular with size 10 m x 10 m x 3 m. The listener is approximately in the center of the space, and the sound source is 2 meters away from the listener. 

## Contributing

Please keep the coding convention.

We are particularly interested in collaborations with Molecular Biologists. Contact enzodesena AT gmail DOT com if interested.


## Authors

* **Enzo De Sena** - [desena.org](https://www.desena.org) (enzodesena AT gmail DOT com)
* **Milton Mermikides** - [Wikipedia page](https://en.wikipedia.org/wiki/Milton_Mermikides)

We are both with the Department of Music and Media, University of Surrey, Guildford, UK [University of Surrey DMM Website](https://www.surrey.ac.uk/department-music-and-media).


## Acknowledgements

We would like to thank Gemma Bruno (Telethon Institute of Genetics and Medicine, Italy) and Niki Loverdu (KU Leuven, Belgium)  for the useful discussions on topic. Also, we would like to thank our friends and colleagues for the useful feedback on the presentation.

The project also uses internally:

* **Yauhen Yakimovich**'s *yamlmatlab* [Github repo](https://github.com/ewiger/yamlmatlab)
* **Ken Schutte**'s *MIDI tooldbox* [Website](https://kenschutte.com/midi)

## References

[1] Durbin, R., Eddy, S., Krogh, A., and Mitchison, G. (1998). Biological Sequence Analysis (Cambridge University Press).

[2] H. Hacıhabiboğlu, E. De Sena, Z. Cvetković, J.D. Johnston and J. O. Smith III, "Perceptual Spatial Audio Recording, Simulation, and Rendering," IEEE Signal Processing Magazine vol. 34, no. 3, pp. 36-54, May 2017.

[3] E. De Sena, Z. Cvetković, H. Hacıhabiboğlu, M. Moonen, and T. van Waterschoot, "Localization Uncertainty in Time-Amplitude Stereophonic Reproduction," IEEE/ACM Trans. Audio, Speech and Language Process. (in press).

[4] E. De Sena, H. Hacıhabiboğlu, and Z. Cvetković, "Analysis and Design of Multichannel Systems for Perceptual Sound Field Reconstruction," IEEE Trans. on Audio, Speech and Language Process., vol. 21 , no. 8, pp 1653-1665, Aug. 2013. 

[5] E. De Sena, H. Hacıhabiboğlu, Z. Cvetković, and J. O. Smith III "Efficient Synthesis of Room Acoustics via Scattering Delay Networks," IEEE/ACM Trans. Audio, Speech and Language Process., vol. 23, no. 9, pp 1478 - 1492, Sept. 2015.


## License

This project is licensed under the GNU License. The code will be made available soon. In the meantime, contact enzodesena AT gmail DOT com if interested. 

You use the code, data and findings here at your own risk. See the [LICENSE.md](LICENSE.md) file for details. 
