# README

This directory contains:
- Reads files from FusionCatcher (see description below)
- Output files from `fusionreport` (see description inside directory)

## NOTE: This dataset and results were taken from project [Fusioncatcher](https://github.com/ndaniel/fusioncatcher/tree/master/test).

The files:
- reads_1.fq.gz
- reads_2.fq.gz

contain a small selection of short reads from:

[1]  SRR1548811 dataset (sample replicate 2, concentration log10 (pMol) = -8,57);
     SRA database http://www.ncbi.nlm.nih.gov/sra/?term=SRR1548811
     article: W.B. Tembe et al., Open-access synthetic spike-in mRNA-seq data
     for cancer gene fusions, BMC Genomics 2014, and

[2] RT-4 bladder cell line from Cancer Cell Line Encyclopedia,
     https://gdc-portal.nci.nih.gov/legacy-archive/files/dc45e1c0-e048-40b5-b48c-8caf3a7bc5ad

[3] EOL-1 acute myeloid leukemia cell line from Cancer Cell Line Encyclopedia,
     https://gdc-portal.nci.nih.gov/legacy-archive/files/f8df0beb-ac7f-450f-aa61-eef082f642ae

[4] U-118MG glioblastoma cell line from Cancer Cell Line Encyclopedia,
     https://gdc-portal.nci.nih.gov/legacy-archive/files/2c1a4f66-567b-46e0-9849-a869ac47ffc2

[5] Homo sapiens isolate case 2 IGH (D2-21)/MALT1 reciprocal breakpoint junction 
    genomic sequence, Accession GQ406059,
     http://www.ncbi.nlm.nih.gov/nuccore/GQ406059

[6] MUTZ-5 pre-B cell acute lymphoblastic leukemia cell line from Cancer 
    Cell Line Encyclopedia,
     https://gdc-portal.nci.nih.gov/legacy-archive/files/b82fb337-1b52-4146-b3a8-7878422a8027

[7] NALM-6 pre-B cell acute lymphoblastic leukemia cell line from Cancer 
    Cell Line Encyclopedia,
     https://gdc-portal.nci.nih.gov/legacy-archive/files/6fa77b04-bb16-49c5-8033-79dd76860c97

[8] SU-DHL-1 anaplastic large cell lymphoma cell line from Cancer Cell Line 
    Encyclopedia,
     https://gdc-portal.nci.nih.gov/legacy-archive/files/d6f97294-6cdd-4343-b40d-8277df996576

[9] Homo sapiens capicua-like protein/double homeodomain 4 fusion protein 
    (CIC/DUX4 fusion) mRNA, complete cds, Accession DQ388764,
     https://www.ncbi.nlm.nih.gov/nuccore/DQ388764.1

These short reads were selected manually such that they cover 17 already known fusion 
genes, which are:

- FGFR3-TACC3  (short reads from [2])
- FIP1L1-PDGFRA  (short reads from [3])
- GOPC-ROS1  (short reads from [4])
- EWS-ATF1  (short reads from [1])
- TMPRSS2-ETV1  (short reads from [1])
- EWS-FLI1  (short reads from [1])
- NTRK3-ETV6  (short reads from [1])
- CD74-ROS1  (short reads from [1])
- HOOK3-RET  (short reads from [1])
- EML4-ALK  (short reads from [1])
- AKAP9-BRAF  (short reads from [1])
- BRD4-NUT  (short reads from [1]) 
- MALT1-IGH  (short reads from [5])
- IGH-CRLF2  (short reads from [6])
- DUX4-IGH  (short reads from [7])
- NPM1-ALK  (short reads from [8])
- CIC-DUX4  (short reads from [9])

## STAR output

The following files have been created using the following star command (with the [star index](https://github.com/nf-core/test-datasets/raw/refs/heads/modules/data/genomics/homo_sapiens/genome/index/star/star.tar.gz) fetched from the modules branch):

```bash
STAR \
     --genomeDir star \
     --readFilesIn reads_1.fq.gz reads_2.fq.gz \
     --outFileNamePrefix test. \
     --outReadsUnmapped None  \
     --outSAMstrandField intronMotif \
     --chimOutJunctionFormat 1 \
     --twopassMode None \
     --outFilterMultimapNmax 50 \
     --chimMultimapNmax 50 \
     --quantMode GeneCounts \
     --outSAMunmapped Within \
     --readFilesCommand zcat  \
     --alignSJstitchMismatchNmax 5 -1 5 5 \
     --outSAMtype BAM SortedByCoordinate \
     --chimSegmentMin 10 \
     --peOverlapNbasesMin 10 \
     --alignSplicedMateMapLminOverLmate 0.5 \
     --chimJunctionOverhangMin 10 \
     --chimScoreJunctionNonGTAG 0 \
     --chimScoreDropMax 30 \
     --chimScoreSeparation 1  \
     --chimSegmentReadGapMax 3 \
     --chimOutType Junctions WithinBAM \
     --outSAMattrRGline 'ID:test' 'SM:test'
```

`reads_1.fq.gz` and `reads_2.fq.gz` are the fastq files present in this branch (`rnafusion`)

- `test.Aligned.sortedByCoord.out.bam`
     - output from STAR
- `test.Aligned.sortedByCoord.out.bam.bai`
     - created with `samtools index test.Aligned.sortedByCoord.out.bam`
- `test.Aligned.sortedByCoord.out.cram`
     - created with `samtools view -C -T <path_to_fasta_in_modules_branch> --output test.Aligned.sortedByCoord.out.cram test.Aligned.sortedByCoord.out.bam`
- `test.Aligned.sortedByCoord.out.cram.crai`
     - created with `samtools index test.Aligned.sortedByCoord.out.cram`
- `test.Chimeric.out.junction`
     - output from STAR
- `test.SJ.out.tab`
     - output from STAR


