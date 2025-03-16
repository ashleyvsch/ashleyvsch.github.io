---
layout: archive
title: "Research"
permalink: /research/
author_profile: true
header:
  overlay_color: '#5e7783'
---

{% include base_path %}


# Overview 
<!-- {: .text-center} -->

Environmental pollutants continue to pose significant threats to human health, development, and ecosystems. Identifying the most harmful pollutants and understanding the mechanisms through which they exert their effects remains a key focus of developmental and environmental toxicology. As a computational scientist, my goal is to contribute to these efforts by developing mathematical and computational tools that elucidate toxicant-induced effects during embryonic development.
{: .text-justify}

I collaborate closely with Dr. Karilyn Sant at the School of Public Health, San Diego State University (SDSU), who investigates the impacts of common water pollutants using the zebrafish model (Danio rerio). Together, with the support of Dr. Uduak George from SDSU's Department of Mathematics and Statistics, we validate the tools I develop, combining experimental data with advanced mathematical modeling. This interdisciplinary collaboration has led to the successful exploration of various environmental contaminants and their impacts.
{: .text-justify}


<hr>

# Research Highlights
<!-- {: .text-center} -->

## Birth Defects, Environmental Exposures, and Machine Learning

Birth defects arise from a complex interplay of genetic, environmental, and maternal factors. My research employs multilayer network analysis and machine learning to uncover hidden patterns in large-scale birth outcome data. By integrating information on maternal health, environmental exposures, and newborn conditions, I aim to:
{: .text-justify}

- Identify high-risk factors associated with specific birth defects.
- Determine co-occurring risk factors across different biological and environmental layers.
- Build predictive models that improve early detection and intervention strategies.

A key finding of my work shows that mothers with birth defects had an increase in variable co-occurrence across layers, supporting the multifactorial nature of birth defects. Additionally, by applying feature selection techniques, I have demonstrated that environmental exposures are critical predictors of adverse birth outcomes.
{: .text-justify}

This research highlights the power of computational approaches to enhance our understanding of maternal-fetal health and improve risk assessment models for birth defects.
{: .text-justify}

## Network Analysis & Machine Learning for Zebrafish Transcriptomics

Toxicant exposure during early development can disrupt key biological pathways, leading to long-term health consequences. To better understand the molecular responses to environmental chemicals, I applied a combination of network-based clustering, gene co-expression analysis, and machine learning to zebrafish transcriptomic data.
{: .text-justify}

Using transcriptomics from zebrafish embryos exposed to a diverse panel of chemicals, my research uncovered:
{: .text-justify}

- Five distinct clusters of toxicant exposures, each linked to specific pancreatic pathway disruptions.
- Gene co-expression networks that reveal shared and unique transcriptional responses across exposure groups.
- Machine learning models that predict cluster membership based on chemical structure and physicochemical properties, identifying key features that drive toxicity.

By integrating network science, functional genomics, and predictive modeling, this work demonstrates how computational toxicology can enhance risk assessment frameworks and provide mechanistic insights into chemical-induced toxicity.
{: .text-justify}

## danRerLib: A Python Package for Zebrafish Transcriptomics
<!-- {: .text-center} -->

<div>
    <div class="align-left">
        <img src="/images/danrerlib_logo.png" >
    </div>
    <p>
        Understanding differential gene expression pathways is crucial for identifying how organisms respond to environmental stressors. Zebrafish, with a transcriptome similar to humans, serve as a valuable model for studying development and disease. However, incomplete zebrafish pathway annotations can limit functional insights. danRerLib addresses this challenge by mapping zebrafish genes to human orthologs, allowing researchers to leverage more comprehensive human annotations. The package provides tools for functional enrichment analysis using up-to-date Gene Ontology (GO) and KEGG databases, offering a broader perspective on experimental results. Available on GitHub and PIP, with detailed documentation and tutorials. To learn more about this project, I recommend checking out the publication, associated documentation, and even a blog post I wrote about the topic with a mini-presentation on the work.
    </p>
</div>
{: .text-justify}

- [danRerLib Publication](https://doi.org/10.1093/bioadv/vbae065)
- [danRerLib Documentation](https://sdsucomptox.github.io/danrerlib/)
- [Blog Post with Video](https://ashleyschwartz.com/posts/2024/05/danrerlib)

## Complex Network Models for TCPMOH Induced Developmental Deformities
{: .text-center}

<div>
    <div class="align-left">
        <img src="/images/tcpmoh.png" >
    </div>
    <p>
        Tris(4cholophenyl)methanol (TCPMOH) is a recently discovered environmental 
        water contaminant with an unknown origin. Although novel, it is highly 
        persistent in the environment, bioaccumulates in marine species, and has 
        been found in human breast milk. The increase in findings of TCPMOH in 
        the environment and human samples poses itself as a possible threat to 
        human development. My primary goal is to describe the effects of TCPMOH 
        during development using the zebrafish model (Danio rerio) and mathematical 
        modeling. Using microscopy, we have captured developmental timepoints to 
        determine deformities in the zebrafish. A complex network model has been developed 
        to analyze the association between deformities and mortality within and between 
        experimental groups. With new environmental contaminants continually being discovered, 
        the network model developed may be applied to determine the morphological damage 
        any new toxicant may have.
    </p>
</div>
{: .text-justify}


## Mathematical Models for Nutrient Absorption and Fish Growth
<!-- {: .text-center} -->

<div>
    <div class="align-left">
            <img src="/images/zebrafish.png">
    </div>
    <p>
        Optimal embryonic development plays a major role in the health of an 
        individual beyond the developmental stage. Nutritional perturbation 
        during development is associated with cardiovascular and metabolic disease 
        later in life. With both nutritional uptake and overall growth being risk 
        factors for eventual health, it is necessary to understand not only the 
        behavior of the processes during development but also their interactions. 
        I have developed ordinary and delay differential equation models to quantify 
        the rate of yolk absorption and its effect on early development of a 
        vertebrate model (Danio rerio). The model has been extended from a control 
        space to a toxicant space to analyze the effects of perfluorooctanesulfonic 
        acid (PFOS).
    </p>
</div>
{: .text-justify}
