H1N1 Genomic Foundation Model Classifier

A deep learning project benchmarking two genomic foundation models — DNABERT-2 and RNA-FM — for classifying the host origin of Influenza A (H1N1) viral sequences.

Built as an MCA Semester 3 Mini-Project at CUSAT.

What This Does

Given a raw nucleotide sequence from Influenza A's Hemagglutinin gene (Segment 4), this project predicts whether the virus originated from a Human, Swine, or Avian host.

It compares two pre-trained transformer models:

DNABERT-2 — pre-trained on multi-species double-stranded DNA using Byte-Pair Encoding
RNA-FM — pre-trained on 23M+ single-stranded RNA sequences with character-level tokenization
My Contributions

This was a two-person project. My specific contributions were:

predict.py — A command-line inference tool that takes a raw sequence, FASTA file, or random test sample and outputs a predicted host with confidence scores
visualize_benchmark.py — An automated script that generates comparison charts (accuracy, F1, precision, recall) across both models
Embedding caching pipeline — Serialized pre-computed feature tensors to disk so training runs in under 2 seconds instead of several minutes per epoch
Key Results
Metric	DNABERT-2	RNA-FM
Test Accuracy	88.46%	86.39%
Macro F1	0.8832	0.8635
Avian Host F1	94.21%	96.08%

RNA-FM outperformed DNABERT-2 specifically on Avian host classification, likely due to its single-nucleotide resolution tokenization preserving point mutations better.

Dataset
Source: NCBI Virus (GenBank)
Target Gene: Influenza A Segment 4 (Hemagglutinin / HA)
Size: 2,250 sequences — 750 Human, 750 Swine, 750 Avian
Split: 70% Train / 15% Validation / 15% Test (seed=42)
Usage
Run inference on a random test sample
bash
python predict.py --sample
Run inference on a raw sequence
bash
python predict.py --seq "ATGAAAGCAATTTTAGTCTTATTTTTT..."
Run inference on a FASTA file
bash
python predict.py --fasta your_sequence.fasta
Generate benchmark comparison charts
bash
python visualize_benchmark.py --show
Tech Stack
Python 3.10+
PyTorch
HuggingFace Transformers
BioPython
Matplotlib / Seaborn
CUDA (optional, falls back to CPU)
Project Structure
h1n1-genomic-classifier/
├── predict.py                  # CLI inference engine
├── visualize_benchmark.py      # Benchmark chart generator
├── rnafm/
│   └── train.py                # RNA-FM training + embedding cache
├── dnabert/
│   └── train.py                # DNABERT-2 training
├── data/
│   └── test.csv                # Test split
└── logs/
    ├── benchmark_comparison.png
    └── per_class_comparison.png
