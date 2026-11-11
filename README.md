# Project 1: Mutation Identification in NGS Data
## Purpose 
This project compares *Schizosaccharomyces pombe* aligned sequencing reads alongside a reference sequence to identify DNA mismatches and analyse differences between untreated control and genotoxic-agent treatment samples.

## How to Run the Program
Run the provided cell setup first to download and load necessary info; 'reference.txt' and 'reads.csv', then run the cells in order.

## Inputs and Outputs
A string of 200-nucleotide as the reference; each row of the CSV containing a read identifier, sample, group and DNA sequence. This program validates reads, explains every mismatch with its one-based position and substituted bases, prints summaries and substitution frequencies and compares the 3 most frequent position mismatches with a two-sided Welch's t-test. Python dictionaries and list of dictionaries for comparisons are returned for the results.

## Code Design
Validation was separated from detection of mismatch so invalid reads are not compared to the reference and validation returns uppercased sequences and a list of errors instead of ignoring bad reads, keeping a record of problematic data from which samples. The analysis function avoids changing the original imported data by creating new dictionaries. For summaries, nested dictionaries store counts by the sample, position and substitution; making it clear to support a random number of samples without hard-coding names. Mismatch positions resolve ties consistently by decreasing frequency and increasing numerical positions. For statistical tests, instead of treating reads as independent replicates, one percentage per biological sample was used and excluded samples with zero valid reads while keeping zero mismatch samples.

## Testing
Lowercase read sequences become valid uppercase and reads containing 'N' and a wrong length reports both errors in a specific order. Mismatches checked on both sequence ends and zero-mismatch reads. Mixed valid and invalid sample data was tested, assuring percentages exclude reads that are invalid, position ties select earlier sites, and statistical comparisons are returned as 'None' when impossible.


