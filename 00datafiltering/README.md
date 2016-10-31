# Data pre-processing

To prepare the data for subsequent analysis by genomeDCA, you need a file with
aligned genomes of organism in question. This method (genomeDCA) is independent
of the alignment method used. For a sample input file, see `example/maela.head`.
    
1. Obtain a multiple sequence alignment of genomes.
2. Prepare an input file, containing the summary statistics, counting the number of occurences of individual allelles at given positions (00summarystatistics.py)

        `Example:
          12004 3110   10    0    0    0   36 0.0000
          |     |       |    |    |    |   |  |
          |     |       |    |    |    |   |  \- Minor allele frequency
          |     |       |    |    |    |   |     (column 2)/(column2+column3)
          |     |       |    |    |    |   \- gap count
          |     |       |    |    |    \- Sanity check - count of letters other than [ACGTN] 
          |     |       |    |    |                      (should be zero)
          |     |       |    |    \- Count of least common allele
          |     |       |    \- Count of third most common allele 
          |     |       \- Count of second most common allele (minor allele), should be non zero
          |     \- Count of most common allele
          \- Position index`
3. Filter the resultant file, to exclude positions that are non bi-allelic, have too low MAF (minor alllele frequency) or too many gaps (01filterstats.py)
4. Encode the results into a pickled Python dictionary for fast access (02encode.py)