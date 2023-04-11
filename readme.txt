A detailed description on installation, usage and current version of PHYRN User Manual can be found at:

http://code.google.com/p/phyrn/

SUPPORT
Please feel free to contact us with your questions, comments and suggestions. Thank you, for your help and support.

Gaurav Bhardwaj (gauravcd34@gmail.com)

Randen L. Patterson (rlpatterson@ucdavis.edu)

Damian B. van Rossum (dbv10@psu.edu)

Citations
If you use PHYRN for your work, please cite:

Bhardwaj G, Ko K, Hong Y, Zhang Z, Ho NL, Chintapalli SV, Kline L, Gotlin M, Hartranft D, Patterson M, Dave F, Smith EJ, Holmes E, Patterson R, van Rossum DB. PHYRN: A Robust Method for Phylogenetic Analysis of Highly Divergent Sequences. PLoS ONE (2012) 7(4): e34261

Step 1: make pssm library
blastpgp -d <nr_database> -i <input file> -o <output_file> -C <matrix outfile> -e 0.01 -m 0 -s T -a 1 -h 1.0e-6 -j 6 -M BLOSUM62 -F F -u 1 -J T
# this "blastpgp" tool has been deprecated and replaced by "psiblast", and as is "formatdb" being replaced by "makeblastdb", and "formatrpsdb" by "makeprofiledb" in blast+

##run psiblast with domain sequence as query and nr as database:
psiblast -db $1 \
	-query $2 \
	-out $3 \
	-out_ascii_pssm $4 \
	-evalue 0.01 \
	-outfmt 0 \
	-use_sw_tback \
	-num_threads 3 \
	-inclusion_ethresh 1.0e-6 \
	-matrix BLOSUM62 \
	-seg no \
	-parse_deflines
  
## summrize the pssm libraries to make a signgle one:
makeprofiledb -i <pssm file list> -o T -n <library name>

Step 2: search full-length queries against the pssm library
rpsblast -i <query file> -d <PSSM Library> -e 1e10 -m 8 -o <output file>
