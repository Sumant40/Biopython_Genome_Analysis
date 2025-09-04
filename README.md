
# COVID-19 Genome Analysis using Biopython

This project demonstrates how to fetch, analyze, and manipulate the COVID-19 genome using **Biopython**.

## Overview

- Fetches the complete SARS-CoV-2 genome from the NCBI database.
- Analyzes nucleotide sequences (length, composition, etc.).
- Uses Biopython modules: **Entrez** (for data retrieval) and **SeqIO** (for parsing sequences).

## Dataset

- **Accession ID**: MN908947.3  
- Source: NCBI Nucleotide Database  
- Description: Severe acute respiratory syndrome coronavirus 2 isolate Wuhan-Hu-1, complete genome.

## Code Explanation

### 1. Fetching the Genome from NCBI
```python
from Bio import Entrez, SeqIO
Entrez.email = "your_email@example.com"  # Required by NCBI

handle = Entrez.efetch(db="nucleotide", id="MN908947", rettype="gb", retmode="text")
recs = list(SeqIO.parse(handle, 'gb'))
handle.close()
```
- **Entrez.efetch()**: Fetches genome data from NCBI.
- **rettype="gb"**: Retrieves data in GenBank format.
- **SeqIO.parse()**: Parses the GenBank record into a sequence object.

### 2. Extracting the Genome Sequence
```python
covid_dna = recs[0].seq
print(f"Length of the genome: {len(covid_dna)}")
```
- Extracts the genome sequence as a `Seq` object.
- Prints the number of nucleotides.

### 3. Analyzing the Genome
You can perform:
- **Length analysis** (number of nucleotides).
- **Base composition**: count of A, T, G, C.
- **Sub-sequence extraction** for specific regions.

Example:
```python
from Bio.SeqUtils import gc_fraction
gc_content = gc_fraction(covid_dna) * 100
print(f"GC Content: {gc_content:.2f}%")
```

### 4. Possible Further Analyses
- Translate the genome into protein sequences.
- Identify open reading frames (ORFs).
- Perform BLAST analysis to compare with other viral genomes.

## Requirements

- Python 3.x
- Biopython (`pip install biopython`)
- Internet access (to fetch data from NCBI)

## How to Run

1. Install dependencies:
```bash
pip install biopython
```

2. Set your email in the `Entrez.email` field (mandatory for NCBI requests).

3. Run the notebook or script to fetch and analyze the genome.

## References

- [NCBI GenBank Accession: MN908947.3](https://www.ncbi.nlm.nih.gov/nuccore/MN908947)
- Biopython documentation: [https://biopython.org/wiki/Documentation](https://biopython.org/wiki/Documentation)

## License

Open-source and free to use for research and educational purposes.
