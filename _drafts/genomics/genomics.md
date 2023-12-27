---
layout: post
title: "Genomics"
category: jekyll update
---

### 1.1 Origin of Replication (oriC)
In Replication a enzyme called DNA Polymerase works and it needs a protein DnaA. DnaA binds to a short nucleotide region, typically 9 nucleotides, in origin of replication called DnaA box. DnaA protein actually wants to see multiple DnaA box to bind efficiently.  

#### 1.1.1 Frequent Word Problem: 
Given k and string of length L, find the most frequent k-mer in L.

#### 1.1.2 Clump Finding Problem: 
Given k, L, t and a string >= L (representing genome), Find (L, t)-Clumps that may be possible replication origin. That is k-mer that appears t times in window length of at least L.

From Clump finding problem we may find thousands of such clump that are potential oriC. 

DNA is bidirectional but each strands are unidirectional. DNA polymerase is also unidirectional that is it can only replicate in the reverse direction of the DNA strand. There are 2 forward half-strands and 2 reverse half-strands in the DNA. The reverse half-strands are easy to replicate and spend most of their lifetime as double stranded. But the other 2 forward half-strands are difficult to replicate. As DNA unwind a small chunk is replicated in the reverse direction each time that are called okazaki fragments. They are repaired to become a single strand afterwards.

It is found that most mutation occurs from C mutating to T. And also in  single-stranded nucleotide mutation is higher than double-stranded nucleotide, Actually C mutates to T in single-stranded nucleotide in 100% rate. So in a reverse half-strand G-C is high and in forward half strand G-C is low. So if we go through DNA counting G-C and find sudden increase in the (G-C) we may have found the region of replication.

#### 1.1.3 Skew Diagram:
We find skew(k) = #G-#C for each k-mers and plot it against k. From the diagram we may find the oriC from the global minima. 

But running Frequent Word algorithm in the k-mer from the local minima we do not find DnaA box. There might be variation in the DnaA bix.

#### 1.1.4 Frequent Word with Variation Problem:
Given k, d and string of length L, find the k-mer with at most number of defect d in string L.

### 1.2 Regulatory Motifs
In plant there are only 3 regulatory gene in plants that controls the circadian behavior - CCA1, LCY, TOC1. These proteins are also called transcription factor and binds in the upstream region of genes to control their expressions. How do these protein know where to bind in the gene? - the genes probably has pattern where these protein can bind.

#### 1.2.1 Implemented Motif Problem:
Given k, d and a set of strings, find the (k, d)-mer/motif that occurs most in the given strings. A (k, d)-mer/motif is a string of length k with at most d defects in it.

The problem is the in real life biological system (e.g - bacteria) it is not true that we will get such (k, d)-mer in every string, that is, in the upstream region of the genes. In such case we go from motif matrix to consensus motif. We have a set of motifs formed in a matrix. The most occurred nucleotide in a position is written in capital and any other nucleotide are written in small letter. The consensus motif is the motif with the capital letter nucleotide in each position from the motif matrix. There is a motif logo that represent such motif matirx. The score of this motif matrix is the sum of number of small letter nucleotides in each position. 

#### 1.2.2 Motif Finding Problem:
Given k and a set of strings, find a single k-mer/motif from each string so that the score of the motif matrix is smaller.

For t number of n-length strings this algorithm needs to calculate score for (n - k +1) ^ t motif matrices with a k * t operation. So overall time complexity is O(n^t * k * t). We can see that the score of motif matrix is the Hamming distance between the consensus matrix and the motif matrix. So, we need to redefine the problem -

#### 1.2.3 Equivalent Motif Finding Problem:
Given k and a set of strings, find a single k-mer/motif from each string so that the score of the motif matrix is smaller.

#### 1.2.4 Median String Problem
