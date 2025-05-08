---
layout: collection-archive
title: "Research"
permalink: /research/
author_profile: true
header:
  overlay_color: '#5e7783'
toc: true
---

{% include base_path %}


# Overview 

Environmental pollutants and toxicants pose significant risks to human health and development. Identifying harmful exposures and unraveling their mechanisms of toxicity is critical for public health and regulatory decision-making. My research lies at the intersection of computational modeling, network science, and machine learning, where I develop and apply mathematical and data-driven approaches to uncover toxicant-induced effects during embryonic development.
{: .text-justify}

I work closely with Dr. Karilyn Sant, Michigan State University Department of Pharmacology and Toxicology, whose lab investigates the effects of common pollutants using zebrafish (Danio rerio) as a model system. Additionally, under the guidance of Dr. Uduak George from SDSU’s Department of Mathematics and Statistics, I integrate computational, statistical, and machine learning methods to extract biological insights from complex datasets.
{: .text-justify}

Through this interdisciplinary collaboration, I have built network-based and predictive models that enhance our ability to identify key toxicants, determine their mechanisms of action, and predict potential health imp
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

This research highlights the power of computational approaches to enhance our understanding of maternal-fetal health and improve risk assessment models for birth defects. The finding of this work have currently been submitted for publication.
{: .text-justify}

## Network Analysis & Machine Learning for Zebrafish Transcriptomics

Toxicant exposure during early development can disrupt key biological pathways, leading to long-term health consequences. To better understand the molecular responses to environmental chemicals, I applied a combination of network-based clustering, gene co-expression analysis, and machine learning to zebrafish transcriptomic data.
{: .text-justify}

Using transcriptomics from zebrafish embryos exposed to a diverse panel of chemicals, my research uncovered:
{: .text-justify}

- Five distinct clusters of toxicant exposures, each linked to specific pancreatic pathway disruptions.
- Gene co-expression networks that reveal shared and unique transcriptional responses across exposure groups.
- Machine learning models that predict cluster membership based on chemical properties, identifying key features that drive toxicity.

By integrating network science, functional genomics, and predictive modeling, this work demonstrates how computational toxicology can enhance risk assessment frameworks and provide mechanistic insights into chemical-induced toxicity. This work has recently been accepted for publication in _Toxicological Sciences_ and is currently in press.
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

# Collaborative Research

Beyond my primary research in computational toxicology, I have contributed to interdisciplinary projects as a computational lead that leverage RNA-Seq, other -omics data, and a variety of biological endpoints to uncover molecular mechanisms underlying disease.

## Investigating IDH1 Mutations in Tumor Models

One such collaboration explored how mutations in isocitrate dehydrogenase 1 (IDH1) impact tumor development through epigenetic and transcriptomic alterations. As part of this work, I conducted RNA-Seq data analysis, helping to identify key gene expression changes associated with different IDH1 mutations. Our findings demonstrated that:
{: .text-justify}

- IDH1 R132Q mutants exhibit higher catalytic efficiency for producing the oncometabolite D-2-hydroxyglutarate (D2HG) compared to R132H mutants.
- This difference in D2HG levels correlates with distinct DNA methylation patterns, particularly in DNA damage and repair pathways.
- Transcriptomic profiling revealed differential activation of oncogenic pathways, including EGFR and PI3K signaling, suggesting IDH1 R132Q may drive a more aggressive tumor phenotype.

This work highlights the power of transcriptomics and multi-omics approaches in uncovering mechanistic insights into cancer biology.
{: .text-justify}

## Spatial Transcriptomics Reveals Macrophage Heterogeneity in Vaping-Associated Lung Inflammation

Spatial Transcriptomics Reveals Macrophage Heterogeneity in Vaping-Associated Lung Inflammation
In collaboration with pulmonary biology researchers, I applied spatial transcriptomics and machine learning to investigate how chronic exposure to vape juice alters macrophage behavior in the lungs. Using mouse models exposed to vape aerosols over nine weeks, we analyzed gene expression in the context of whole-lung architecture, enabling spatially resolved profiling of immune responses.
{: .text-justify}

Key findings from this project include:
- Identification of macrophage-expressed genes—Myl4, Myl7, Bpifa1, and Hbb-bs—that robustly distinguish vaped from control lungs.
- Machine learning models (Random Forest, LASSO logistic regression) revealed gene signatures linked to chronic vaping exposure and highlighted sex-specific transcriptional responses.
- Spatial network analysis uncovered microenvironment-specific pathway alterations, indicating that macrophage function is not uniform across lung regions.
- Both male and female vaped mice exhibited distinct inflammatory pathway activity, suggesting vaping broadly disrupts immune homeostasis in the lung.

This work underscores the importance of spatially resolved transcriptomic analysis in understanding immune heterogeneity and the biological consequences of vaping. The results of this work is currently in preparation for publication.
{: .text-justify}

## Quantifying Pulmonary Inflammation in Viral Infections

As part of a collaborative study on acetylcholine’s role in immune regulation during influenza infection, I developed an automated image processing algorithm to quantify inflammation in lung tissue. This work involved:
{: .text-justify}

- Developing an image analysis pipeline to process Iba1 immunofluorescence images, allowing for objective, high-throughput quantification of immune cell activity.
- Automating macrophage activation scoring, reducing subjectivity and manual effort compared to traditional histological methods.
- Applying the method to study the effects of acetylcholine inhibition on pulmonary inflammation, showing that ACh depletion led to increased inflammation and impaired tissue repair.

This approach highlights the power of computational image analysis in immunology and disease pathology, enabling precise, reproducible quantification of biological processes. This work is currently published and can be found [here](https://www.tandfonline.com/doi/full/10.2147/ITT.S279228).
{: .text-justify}