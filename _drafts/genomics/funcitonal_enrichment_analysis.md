---
layout: post
title: "Functional Enrichment Analysis"
category: jekyll update
---

> a.k.a pathway analysis/signature analysis is a method to identify a class of genes/proteins that are over-represented within a larger set of genes/proteins, and may have been associated with a disease phenotypes. In short it is about finding what is a set of differential genes doing.

There are many approaches for functional enrichment analysis - 
- Gene Ontology (GO): A structured vocabulary for describing gene function. In this vocabulary >50,000 genes are annotated with term ~100,000 term-term relation for human. It actually forms a directed acyclic graph (DAG). It is manually curated and often redundant.
- Requires pre-selection of genes
- Does not require any additional data related to the genes
- User does not control vocabulary
There are 3 different ontology -
a. Cellular Component (CC): Where is the gene product localized?
b. Biological Process (BP): What function does is perform in that location?
c. Molecular Function (MF): How does it carry out that function (by which molecular mechanism)?
- Gene Set Enrichment Analysis (GSEA):
  - Does not require pre-selection of gene
  - Require both gene identifier and related data
  - User can control vocabulary

- Over Representation Analysis (ORA):
hyper geometric/ Fisher’s exact test 