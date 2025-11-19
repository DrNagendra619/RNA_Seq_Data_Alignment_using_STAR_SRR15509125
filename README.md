# RNA_Seq_Data_Alignment_using_STAR_SRR15509125
RNA_Seq_Data_Alignment_using_STAR_SRR15509125
# 🧬 STAR RNA-Seq Alignment Workflow (SRR15509125 on Human Chromosome 22)

This repository contains a comprehensive **Jupyter Notebook** pipeline for performing **RNA-Seq read alignment** using the ultra-fast aligner, **STAR** (Spliced Transcripts Alignment to a Reference).

The workflow demonstrates best practices for handling public RNA-Seq data by fetching a specific accession (**SRR15509125**), preparing a subset of the reference genome (**Human Chromosome 22**), generating the STAR index, performing the alignment, and analyzing the resulting quality control (QC) log file.

## 🚀 Key Features

* **Complete End-to-End Pipeline:** Covers environment setup, data download, reference preparation, indexing, alignment, and QC visualization.
* **STAR Implementation:** Uses the robust STAR aligner (version 2.7.10a) to align spliced reads.
* **Targeted Reference:** Aligns reads to a specific, reduced reference (**Human GRCh38, Chromosome 22**) for focused analysis or rapid prototyping.
* **Data Source:** Downloads paired-end reads directly from the **SRA database** using the `sra-toolkit`.
* **Integrated QC Visualization:** Parses the STAR log file and generates an interactive **Plotly Bar Chart** to visualize read mapping statistics (unique, unmapped, and multi-mapping rates).
* **Output Formats:** Generates industry-standard output files: **Sorted BAM** (for visualization/variant calling) and **ReadsPerGene.out.tab** (for Differential Expression Analysis).

---

## 🔬 Analysis Steps

The notebook is structured into the following executable steps:

1.  **Environment Setup:** Installs necessary tools (`sra-toolkit`) and compiles the `STAR` aligner.
2.  **Data Download:** Fetches and extracts paired-end FASTQ files for the accession **SRR15509125** from the SRA database.
3.  **Reference Preparation:** Downloads the FASTA and GTF files for **Human Chromosome 22** (Ensembl GRCh38).
4.  **Genome Indexing:** Runs `STAR --runMode genomeGenerate` to create the alignment index.
5.  **Read Alignment:** Executes `STAR --runMode alignReads` to align the FASTQ files, producing a coordinate-sorted BAM file and gene counts (`--quantMode GeneCounts`).
6.  **QC & Plotting:** Parses the **`Log.final.out`** file and generates an interactive **Plotly Bar Chart** summarizing read mapping percentages.

## ⚠️ Key Findings from Alignment Log (QC)

The alignment results for **SRR15509125** against only Human Chromosome 22 highlight significant issues:

* **Extremely Low Unique Mapping Rate:** Only **0.00%** of input reads uniquely mapped.
* **High Unmapped Reads:** Nearly all reads are unmapped, split between:
    * **48.22%** unmapped due to being **too short**.
    * **51.78%** unmapped for **other reasons**.
* **Low Mapping Speed:** The alignment was slow, running at only **0.30 million reads per hour**.

**Assessment:** This performance indicates that the reads are almost certainly not from Chromosome 22. The low unique mapping and high unmapped rates suggest the reads are either from the full human genome or a different species/organism entirely. The high average input read length (458 bp) combined with the "too short" unmapped percentage suggests reads were likely heavily trimmed, or the data quality is poor.

---

## 🛠️ Prerequisites and Execution

### Requirements

To run this pipeline, you need access to a Linux environment with the following tools (which the script installs):

* **`sra-toolkit`** (for `prefetch` and `fasterq-dump`)
* **`STAR`** (version 2.7.10a)
* **Python** libraries: `pandas`, `plotly.graph_objects`

### How to Run

1.  Open the **`RNA_Seq_Data_Alignment_using_STAR_SRR15509125.ipynb`** file in Google Colab or a Jupyter environment.
2.  Execute all cells sequentially.
3.  The final cells will output the alignment metrics and display the interactive Plotly visualization.

---

## 📁 Output Files

The pipeline generates the following key files in the `star_output/` directory:

| Filename | Format | Description |
| :--- | :--- | :--- |
| `SRR15509125_Aligned.sortedByCoord.out.bam` | BAM | The primary alignment file, sorted by genomic coordinate. |
| `SRR15509125_ReadsPerGene.out.tab` | TSV | Gene count matrix quantified using the provided GTF annotation. |
| `SRR15509125_Log.final.out` | Text | Detailed log of alignment metrics, used for quality control. |
