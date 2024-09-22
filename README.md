<div align="center">
    <h1>PolyGenNet-</h1>
    
</div>


# Introduction

PolyGenNet- is a computational framework designed to analyze and visualize **gene-gene interaction networks** in the context of complex human traits. The platform integrates multiple datasets to uncover trait-specific variations in gene interactions and provides an accessible interface for both exploratory analysis and hypothesis-driven research.


## Article Related to PolyGenNet-

**Title**: 
Trait-Specific Variations in Gene Interaction Networks Underlying Complex Human Traits  

**Authors**: 
Ehsan Tamandeh, Johannes Schumacher, Carlo Maj, Pouria Dasmeh


## 
This project is inspired by and associated with the research presented in the paper **Trait-Specific Variations in Gene Interaction Networks Underlying Complex Human Traits**. 

The work explores the interplay between gene networks and complex human traits, revealing trait-specific patterns of genetic interaction. 

We then wanted to see whether the characteristics  we observed between **associated and non-associated** networks also extend to a broader spectrum of complex traits.  



The repository contains tools and scripts used in the analysis of this study.

## Why Network Analysis?

Network analysis provides a powerful framework for uncovering more layers of information in complex biological systems. It enables us to abstract relationships between genes and proteins, predict interactions among traits, and study the underlying mechanisms of complex diseases. By mapping biological elements as nodes and their interactions as edges, this approach offers a simplified yet comprehensive view of how these components are interconnected. Through network structures, we can uncover hidden patterns and important associations, ultimately gaining deeper insights into biological processes. This approach guides the discovery of new biomarkers, drug targets, and therapeutic pathways, contributing to advancements in personalized medicine and our overall understanding of biological systems.


## Associated Gene-Gene Interaction Networks examples: 
<div style="display: flex; gap: 10px;">
  <img src="graph_plot_3342.png" alt="Associated Gene-Gene Interaction Networks 1" width="300"/>
  <img src="graph_plot_3412.png" alt="Associated Gene-Gene Interaction Networks 2" width="300"/>
</div>

## Non-associated Gene-Gene Interaction Networks examples: 
<div style="display: flex; gap: 10px;">
  <img src="graph_plot_13.png" alt="Non-associated Gene-Gene Interaction Networks 3" width="300"/>
  <img src="graph_plot_11.png" alt="Non-associated Gene-Gene Interaction Networks 4" width="300"/>
</div>

For further reading, you can refer to the full article [here](link-to-the-article).

## Table of Contents
- [Project Overview](#Project_Overview)
- [Installation](#installation)
- [Features](#features)
- [Contact](#contact)
- [Results](#results)

## Project Overview

Our analysis began with the compilation of gene names and their associations with various traits using **Genome-Wide Association Studies (GWAS)**. 
To evaluate the strength of these associations, we employed confidence scores: scores below 0.4 indicate a weak association, scores around 0.7 suggest a moderate association, and scores above 0.9 denote a strong association between a gene and a trait.

Focusing on traits with high-confidence gene associations, we identified those with at least 60 genes scoring above 0.9, which refined our analysis to 461 traits out of the 4,756 initially available in the GWAS data. The dataset also included a total of 20,188 genes.

To construct the interaction networks for each trait, we calculated the gene-gene interaction network adjacency matrix using the GWAS data. This matrix provided a detailed statistical representation of the interactions within each network. For further validation and visualization, we also utilized data from the STRING database.

<img src="Untitled.png" alt="Untitled.png" width="800"/>

## Analysis Scheme Overview :

**Gene Selection:**

We categorized genes based on their confidence scores. 
Genes with the highest scores in a trait were labeled as **"associated genes"**, while those with lower scores were termed **"non-associated genes"**.




**Interaction Compilation:** 

We gathered all possible gene interactions for each selected trait using GWAS, ensuring a comprehensive representation of gene interactions across a wide range of organs and biological systems.
Network Analysis: We analyzed the structure of these gene-gene interaction networks by calculating the number of "interactions" within the network. This analysis allowed us to distinguish between "connected genes," which represent genes that interact with others, and "isolated genes," representing genes without interactions.




**Comparative Analysis:** 

For each trait, we calculated two sets of values—one for associated genes and another for non-associated genes—covering the **number of connected genes, isolated genes, gene-gene interactions, and the highest degree** within the network. Comparing these values enabled us to draw insights into the differences in network structures between associated and non-associated genes.




**Degree Distribution and Network Structure:** 

We investigated the degree distribution of connected and isolated genes to better understand the network dynamics. 
The degree distribution analysis was essential for exploring the relationship between connected and isolated genes within these networks.
Network Structure Identification: To determine the optimal network structure, we applied the Akaike Information Criterion (AIC) method. By evaluating the AIC values for various potential structures and selecting the one with the lowest AIC, we identified the most appropriate network structure for each trait's gene-gene interaction network.




## Installation

To install and set up the PolyGenNet- framework on your local machine, follow these steps:

### 1. GWAS Summary Statistics from the Atlas of GWAS 

The [Atlas of GWAS Summary Statistics](https://atlas.ctglab.nl/) is a rich database containing publicly available Genome-Wide Association Study (GWAS) summary statistics. Currently, the database includes:

- **4,756 GWAS** from **473 unique studies**
- Covering **3,302 unique traits** across **28 domains**

This resource allows users to explore GWAS via manhattan plots, risk loci, gene-based MAGMA results, SNP heritability, and genetic correlations with other GWAS in the database. Many of these datasets are based on UK Biobank release 2 data under application ID 16406.

**Download Full MAGMA Gene P-values**

You can download the full MAGMA gene P-values from *Database Release 3: v20191115* [here](https://atlas.ctglab.nl/).


### 2. STRING db

The [STRING db](https://www.string-db.org) is a database of known and predicted protein-protein interactions. The interactions include direct (physical) and indirect (functional) associations. The database contains information from numerous sources, including experimental repositories, computational prediction methods and public text collections. Each interaction is associated with a combined confidence score that integrates the various evidences.

To install the "STRING db" package, start R (version "4.4") and enter:
   ```bash
   if (!require("BiocManager", quietly = TRUE))
       install.packages("BiocManager")

   BiocManager::install("STRINGdb")
   ```

### 3. gprofiler package

The **"g:Convert"** is a feature within the "gprofiler" package suite that allows for mapping between different biological identifiers such as genes, proteins, microarray probes, and database-specific identifiers. 
It supports mapping across numerous databases (e.g., Ensembl, UniProt, NCBI, etc.) and for a wide range of species.

Key Use Cases of g:Convert:
   
Gene/Protein Identifier Conversion: Map identifiers across different formats, like converting Ensembl gene IDs to gene symbols or UniProt IDs.
Cross-Species Mapping: Transfer gene/protein information from one organism to another when homologous relationships are known.
Unifying Data Sources: Standardize identifiers when working with datasets from different sources that use varied naming conventions.
   
Example Mappings:
Gene to Protein ID: Convert gene symbols (like BRCA1) to corresponding UniProt or Ensembl IDs.
Microarray Probes to Gene Symbols: Map probe IDs from microarray data to gene names for further analysis.

To install the "g:Profiler" package in R enter:
   ```bash
   install.packages("gprofiler2")
   ```


## Features

In gene interaction networks, genes and gene products interact with each other through physical and functional connections, forming complex networks. 
These networks exhibit properties such as modularity and scale-free topology, where a few highly connected genes (hubs) play critical roles in maintaining cellular functions. 
Variations in these hubs or their interactions can have cascading effects on the network, leading to phenotypic changes associated with diseases. For instance, genes involved in Schizophrenia (SCZ) or other complex diseases often participate in common pathways or modules within the gene interaction network, even though the specific mutations may differ across patients.

## Results

The following table summarizes key metrics related to gene networks for several traits, comparing associated and non-associated networks to reveal significant differences in gene connectivity and interaction dynamics.

![3 examples](https://drive.google.com/uc?id=1vfZz4MJL_NpgfvOHEiW4-zspkDcJMm_w)

The table presents an analysis of gene networks associated with various traits, illustrating the differences between associated and non-associated networks. This comparative approach highlights how traits linked to specific conditions, such as schizophrenia, Crohn's disease, and coronary artery disease, tend to exhibit greater connectivity among genes. In associated networks, a higher number of connected genes and gene-gene interactions are observed, indicating a more intricate web of relationships that may underlie the biological mechanisms of these traits. Conversely, non-associated networks show fewer connections, suggesting a potential lack of significant interaction among the genes in these cases.

The average data for all analyzed traits reinforce this trend, with associated traits generally demonstrating a more complex network structure, as evidenced by the larger number of connected genes and interactions. Additionally, the slope of the degree distribution on log-log scales indicates that associated networks maintain a more substantial presence of highly connected genes, which can be crucial for understanding the functional roles of these genes in disease processes. Overall, this analysis underscores the importance of network connectivity in elucidating the genetic basis of complex traits, providing insights that could inform future research and therapeutic strategies.

![Scatter Image](https://drive.google.com/file/d/1HzI9DFLjvaj_I0n0DhbkJf0_fs43LPU2/view?usp=drive_link)

## Contact

 Please do not hesitate to contact me if you require any further information: 
 
 Ehsan Tamandeh
 
 Email: ehsan.tamandeh007@gmail.com
 



## Acknowledgments

Special thanks to my supervisors **Prof. Dr. Johannes Schumacher, Dr. Carlo Maj**, and **Dr. Pouria Dasmeh** for their contributions to the research behind this project.
