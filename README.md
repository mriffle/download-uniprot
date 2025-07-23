# download-uniprot

How I like to download all Uniprot sequences:

```
# Download UniProt Trembl in parallel chunks
curl -s --range 0-9999999999 -o file.part1 ftp://ftp.ebi.ac.uk/pub/databases/uniprot/knowledgebase/uniprot_trembl.fasta.gz &
curl -s --range 10000000000-19999999999 -o file.part2 ftp://ftp.ebi.ac.uk/pub/databases/uniprot/knowledgebase/uniprot_trembl.fasta.gz &
curl -s --range 20000000000-29999999999 -o file.part3 ftp://ftp.ebi.ac.uk/pub/databases/uniprot/knowledgebase/uniprot_trembl.fasta.gz &
curl -s --range 30000000000-39999999999 -o file.part4 ftp://ftp.ebi.ac.uk/pub/databases/uniprot/knowledgebase/uniprot_trembl.fasta.gz &
curl -s --range 40000000000-49999999999 -o file.part5 ftp://ftp.ebi.ac.uk/pub/databases/uniprot/knowledgebase/uniprot_trembl.fasta.gz &
curl -s --range 50000000000-59999999999 -o file.part6 ftp://ftp.ebi.ac.uk/pub/databases/uniprot/knowledgebase/uniprot_trembl.fasta.gz &
curl -s --range 60000000000-69999999999 -o file.part7 ftp://ftp.ebi.ac.uk/pub/databases/uniprot/knowledgebase/uniprot_trembl.fasta.gz &
curl -s --range 70000000000-79999999999 -o file.part8 ftp://ftp.ebi.ac.uk/pub/databases/uniprot/knowledgebase/uniprot_trembl.fasta.gz &
curl -s --range 80000000000-89999999999 -o file.part9 ftp://ftp.ebi.ac.uk/pub/databases/uniprot/knowledgebase/uniprot_trembl.fasta.gz &
curl -s --range 90000000000-99999999999 -o file.part10 ftp://ftp.ebi.ac.uk/pub/databases/uniprot/knowledgebase/uniprot_trembl.fasta.gz &

# Download SwissProt separately
curl -s -o uniprot_sprot.fasta.gz https://ftp.uniprot.org/pub/databases/uniprot/current_release/knowledgebase/complete/uniprot_sprot.fasta.gz &

# Wait for all background jobs to complete
wait

# Combine all parts into one final file
cat file.part? uniprot_sprot.fasta.gz > uniprot_trembl_swissprot.fasta.gz

# Clean up intermediate files
rm file.part? uniprot_sprot.fasta.gz
```
