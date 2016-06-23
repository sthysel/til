# Sequence filenames

```
(?P<id>\d{4,6})_
(?P<extraction>\d)_
(?P<libary>PE|MP)_
(?P<size>\d*bp)_
MM_
(?P<vendor>AGRF|UNSW)_
(?P<plate>\w{9})_
(?P<index>[G|A|T|C|-]*)_
(?P<lane>L\d{3})_
(?P<read>R[1|2])\.fastq\.gz
```

Mathes 

```
21655_1_PE_680bp_MM_AGRF_H3VJJBCXX_GTAGAGGA_L001_R2.fastq.gz
21655_1_PE_680bp_MM_AGRF_H3VJJBCXX_GTAGAGGA_L002_R1.fastq.gz
21655_1_PE_680bp_MM_AGRF_H3VJJBCXX_GTAGAGGA_L002_R2.fastq.gz
21675_1_MP_700bp_MM_UNSW_HKL5CBCXX_TAAGGCGA-CTCTCTAT_L001_R1.fastq.gz
21675_1_PE_700bp_MM_UNSW_HKL5CBCXX_TAAGGCGA-CTCTCTAT_L001_R2.fastq.gz
21675_1_PE_700bp_MM_UNSW_HKL5CBCXX_TAAGGCGA-CTCTCTAT_L002_R1.fastq.gz

```
