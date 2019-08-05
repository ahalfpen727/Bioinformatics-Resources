# A continually expanding collection of cancer genomics notes and data

Issues with suggestions and pull requests are welcome!


* [Tools](#tools)
  * [Preprocessing](#preprocessing)
  * [Purity](#purity)
  * [Immune cell deconvolution](#immune-cell-deconvolution)
  * [BRCA](#brca)
  * [TCGA PanCancer](#tcga-pancancer)
  * [Image analysis](#image-analysis)
  * [Clonal analysis](#clonal-analysis)
* [Survival analysis](#suvival-analysis)
  * [Methods to find best cutoff for survival](#methods-to-find-best-cutoff-for-survival)
* [Cancer driver genes](#cancer-driver-genes)
* [Cancer driver mutations](#Cancer-driver-mutations)
* [Drugs](#drugs)
* [Data](#data)
  * [TCGA](#tcga)
* [Methylation](#methylation)
* [Misc](#misc)

## Tools

### Preprocessing

- `cacao` - Callable Cancer Loci - assessment of sequencing coverage for actionable and pathogenic loci in cancer, example of QC report. Data: BED files for cancer loci from ClinVar, CIViC, cancerhotspots. https://github.com/sigven/cacao

### Purity

- `ABSOLUTE` - infers tumor purity, ploidy from SNPs, CNVs. Also detects subclonal heterogeneity.
    - Carter, Scott L., Kristian Cibulskis, Elena Helman, Aaron McKenna, Hui Shen, Travis Zack, Peter W. Laird, et al. “Absolute Quantification of Somatic DNA Alterations in Human Cancer.” Nature Biotechnology 30, no. 5 (May 2012): 413–21. https://doi.org/10.1038/nbt.2203.
    - Aran, Dvir, Marina Sirota, and Atul J. Butte. “Systematic Pan-Cancer Analysis of Tumour Purity.” Nature Communications 6, no. 1 (December 2015). https://doi.org/10.1038/ncomms9971. - TCGA tumor purity estimation using four methods: ESTIMATE, ABSOLUTE, LUMP, IHC, and a median consensus purity estimation. Gene expression correlates with purity and may affect correlation and differential expression detection analyses - big confounding effect.
        - `data/ABSOLUTE_scores.xlsx` - Supplementary Data 1: Tumor purity estimates according to four methods and the consensus method for all TCGA samples with available data. [Source](https://media.nature.com/original/nature-assets/ncomms/2015/151204/ncomms9971/extref/ncomms9971-s2.xlsx)

- `ESTIMATE` (Estimation of STromal and Immune cells in MAlignant Tumor tissues using Expression data) is a tool for predicting tumor purity, and the presence of infiltrating stromal/immune cells in tumor tissues using gene expression data. ESTIMATE algorithm is based on single sample Gene Set Enrichment Analysis and generates three scores: stromal score (that captures the presence of stroma in tumor tissue), immune score (that represents the infiltration of immune cells in tumor tissue), and estimate score (that infers tumor purity). http://bioinformatics.mdanderson.org/main/ESTIMATE:Overview. R package http://bioinformatics.mdanderson.org/estimate/rpackage.html
    - Yoshihara, Kosuke, Maria Shahmoradgoli, Emmanuel Martínez, Rahulsimham Vegesna, Hoon Kim, Wandaliz Torres-Garcia, Victor Treviño, et al. “Inferring Tumour Purity and Stromal and Immune Cell Admixture from Expression Data.” Nature Communications 4 (2013): 2612. https://doi.org/10.1038/ncomms3612. - ESTIMATE - tumor-stroma purity detection. 141 immune and stromal genes. single-sample GSEA analysis. ESTIMATE score as a combination of immune and stromal scores. [Supplementary data](https://www.nature.com/articles/ncomms3612#supplementary-information).
- `data/ESTIMATE_signatures.xlsx` - A gene list of stromal and immune signatures. [Source](https://media.nature.com/original/nature-assets/ncomms/2013/131011/ncomms3612/extref/ncomms3612-s2.xlsx)
- `data/ESTIMATE_scores.xlsx` - A list of stromal, immune, and ESTIMATE scores in TCGA data sets. All cancers, all gene expression plaforms. [Source](https://media.nature.com/original/nature-assets/ncomms/2013/131011/ncomms3612/extref/ncomms3612-s3.xlsx)

- `ISOpureR` - Deconvolution of Tumour Profiles to purify tumor samples. Regression-based, uses purified tumor profile to estimate the proportion of tumor samples. Discussion of overfitting due to overparametrization. https://cran.r-project.org/web/packages/ISOpureR/index.html
    - Quon, Gerald, Syed Haider, Amit G Deshwar, Ang Cui, Paul C Boutros, and Quaid Morris. “Computational Purification of Individual Tumor Gene Expression Profiles Leads to Significant Improvements in Prognostic Prediction.” Genome Medicine 5, no. 3 (2013): 29. https://doi.org/10.1186/gm433.

### Immune cell deconvolution

- `Immunophenogram` - partitioning immune cell types in cancer. https://github.com/mui-icbi/Immunophenogram, https://tcia.at/home
    - Charoentong, Pornpimol, Francesca Finotello, Mihaela Angelova, Clemens Mayer, Mirjana Efremova, Dietmar Rieder, Hubert Hackl, and Zlatko Trajanoski. “Pan-Cancer Immunogenomic Analyses Reveal Genotype-Immunophenotype Relationships and Predictors of Response to Checkpoint Blockade.” BioRxiv, 2016, 056101. - https://tcia.at/ - immune cells in cancers. Estimated using functional GSEA enrichment, and CIBERSORT. Immunophenogram generation: https://github.com/MayerC-imed/Immunophenogram

- `ImmQuant` - Deconvolution of immune cell lineages. http://csgi.tau.ac.il/ImmQuant/downloads.html
    - Frishberg, Amit, Avital Brodt, Yael Steuerman, and Irit Gat-Viks. “ImmQuant: A User-Friendly Tool for Inferring Immune Cell-Type Composition from Gene-Expression Data.” Bioinformatics 32, no. 24 (December 15, 2016): 3842–43. https://doi.org/10.1093/bioinformatics/btw535.

- `TIMER` - a resource to estimate the abundance of immune infiltration of six cell types, the effect on survival. Accounting for tumor purity using CHAT R package. Linear regression to estimate immune cell abundance. Macrophage infiltration predicts worse outcome, including BRCA. Signature genes from microarray, merged with RNA-seq using ComBat for batch removal, filtered. All TCGA processed. All data at http://cistrome.org/TIMER/download.html, tool at https://cistrome.shinyapps.io/timer/
    - Li, Bo, Eric Severson, Jean-Christophe Pignon, Haoquan Zhao, Taiwen Li, Jesse Novak, Peng Jiang, et al. “Comprehensive Analyses of Tumor Immunity: Implications for Cancer Immunotherapy.” Genome Biology 17, no. 1 (22 2016): 174. https://doi.org/10.1186/s13059-016-1028-7.


### BRCA

- `TNBCtype` tool to classify triple negative breast cancer samples (microarray gene expression) into six subtypes, http://cbc.mc.vanderbilt.edu/tnbc/index.php

- `genefu` R package for PAM50 classification and survival analysis. https://www.bioconductor.org/packages/release/bioc/html/genefu.html

### TCGA

- Zhang, Zhuo, Hao Li, Shuai Jiang, Ruijiang Li, Wanying Li, Hebing Chen, and Xiaochen Bo. “A Survey and Evaluation of Web-Based Tools/Databases for Variant Analysis of TCGA Data.” Briefings in Bioinformatics, March 29, 2018. https://doi.org/10.1093/bib/bby023. - The most comprehensive review of TCGA-related tools. Table 3 - List of Web servers and databases. 

- NCI Genomics Data Commons API. https://docs.gdc.cancer.gov/API/Users_Guide/Getting_Started/ - docs. https://github.com/Bioconductor/GenomicDataCommons - R package
    - Shane Wilson, Michael Fitzsimons, Martin Ferguson, Allison Heath, Mark Jensen, Josh Miller, Mark W. Murphy, James Porter, Himanso Sahni, Louis Staudt, Yajing Tang, Zhining Wang, Christine Yu, Junjun Zhang, Vincent Ferretti and Robert L. Grossman. "Developing Cancer Informatics Applications and Tools Using the NCI Genomic Data Commons API." DOI: 10.1158/0008-5472.CAN-17-0598 Published November 2017 http://cancerres.aacrjournals.org/content/77/21/e15

## Image analysis

- `DeepPATH` - Lung cancer image classification using deep convolutional neural network. Classification by tumor type, mutation type. Refs to other image classification studies that use deep learning. GoogleNet inception v3 architecture. Training, validation, testing cohorts (70%, 15%, 15%). Details on image processing. https://github.com/ncoudray/DeepPATH
    - Coudray, Nicolas, Paolo Santiago Ocampo, Theodore Sakellaropoulos, Navneet Narula, Matija Snuderl, David Fenyö, Andre L. Moreira, Narges Razavian, and Aristotelis Tsirigos. “Classification and Mutation Prediction from Non–Small Cell Lung Cancer Histopathology Images Using Deep Learning.” Nature Medicine 24, no. 10 (October 2018): 1559–67. https://doi.org/10.1038/s41591-018-0177-5.


- `IHCount` - IHC-image analysis workflow, https://github.com/mui-icbi/IHCount

- `pathology_learning` - Using traditional machine learning and deep learning methods to predict stuff from TCGA pathology slides. [https://github.com/millett/pathology_learning](https://github.com/millett/pathology_learning)

## Clonal analysis

- `Awesome-CancerEvolution` - list of papers and tools for studying cancer evolution. https://github.com/iron-lion/Awesome-CancerEvolution

- `E-scape` - cancer evolution visualization. Timescape - time series analysis, http://bioconductor.org/packages/release/bioc/html/timescape.html, MapScape - spatial distribution,http://bioconductor.org/packages/release/bioc/html/mapscape.html, CellScape - single-cell phylogenetic, http://bioconductor.org/packages/release/bioc/html/cellscape.html
    - Smith, Maia A., Cydney B. Nielsen, Fong Chun Chan, Andrew McPherson, Andrew Roth, Hossein Farahani, Daniel Machev, Adi Steif, and Sohrab P. Shah. “E-Scape: Interactive Visualization of Single-Cell Phylogenetics and Cancer Evolution.” Nature Methods 14, no. 6 (30 2017): 549–50. https://doi.org/10.1038/nmeth.4303.

- `fishplot` - Create timecourse "fish plots" that show changes in the clonal architecture of tumors. https://github.com/chrisamiller/fishplot

- `MACHINA` - Metastatic And Clonal History INtegrative Analysis. https://github.com/raphael-group/machina 

- `PyClone` - inferring the cellular prevalence of point mutations from deeply sequenced data. http://compbio.bccrc.ca/software/pyclone/

- `clonevol` R package, Inferring and visualizing clonal evolution in multi-sample cancer sequencing. https://github.com/hdng/clonevol
    - Dang, H. X., B. S. White, S. M. Foltz, C. A. Miller, J. Luo, R. C. Fields, and C. A. Maher. “ClonEvol: Clonal Ordering and Visualization in Cancer Sequencing.” Annals of Oncology: Official Journal of the European Society for Medical Oncology 28, no. 12 (December 1, 2017): 3076–82. https://doi.org/10.1093/annonc/mdx517.


- `SciClone` - number and genetic composition of tumor subclones by analyzing the variant allele frequencies of somatic mutations. Excludes CNV regions. https://github.com/genome/sciclone

- `ape` - R package, Analyses of Phylogenetics and Evolution, https://cran.r-project.org/web/packages/ape/index.html

- `DeconstructSig` - Contribution of known SNP cancer mutation signatures to tumor samples. Data from Alexandrov, COSMIC, others. https://github.com/raerose01/deconstructSigs 



## Survival analysis

- `cBioPortal` - The cBioPortal for Cancer Genomics provides visualization, analysis and download of large-scale cancer genomics data sets. OncoPrint mutation plots, differential expression, coexpression, survival. Compare gene expression with copy number variation. http://www.cbioportal.org/

- `R2` - Genomics Analysis and Visualization Platform. Gene-centric, survival analysis, collection of preprocessed microarray studies. http://hgserver1.amc.nl/

- `KM plotter` - Gene-centric, customizable survival analysis for breast, ovarian, lung, gastric cancers. http://kmplot.com/
    - Györffy, Balazs, Andras Lanczky, Aron C. Eklund, Carsten Denkert, Jan Budczies, Qiyuan Li, and Zoltan Szallasi. “An Online Survival Analysis Tool to Rapidly Assess the Effect of 22,277 Genes on Breast Cancer Prognosis Using Microarray Data of 1,809 Patients.” Breast Cancer Research and Treatment 123, no. 3 (October 2010): 725–31. https://doi.org/10.1007/s10549-009-0674-9.

- `The Human Protein Atlas` - Gene- and protein expression data in multiple cancer tissues, cell lines. Easy one-gene search, summary of tissue-specific expression, survival significance. http://www.proteinatlas.org/
    - Uhlen, Mathias, Cheng Zhang, Sunjae Lee, Evelina Sjöstedt, Linn Fagerberg, Gholamreza Bidkhori, Rui Benfeitas, et al. “A Pathology Atlas of the Human Cancer Transcriptome.” Science (New York, N.Y.) 357, no. 6352 (August 18, 2017). doi:10.1126/science.aan2507. http://science.sciencemag.org/content/357/6352/eaan2507. Rich downloadable data - tissue-specific gene expression in cancer and normal, isoform expression, protein expression. http://www.proteinatlas.org/about/download. Supplementary material http://science.sciencemag.org/content/suppl/2017/08/16/357.6352.eaan2507.DC1  
        - `Table S2` - summary of tissue specific expression for each gene, in normal and cancer tissues.  
        - `Table S6` - summary of survival prognostic value, with a simple "favorable/unfavorable" label for each gene. Each worksheet corresponds to a different cancer.  
        - `Table S8` - per-gene summary, in which cancers it is prognostic of survival.  

- `PRECOG` - PREdiction of Clinical Outcomes from Genomic Profiles. Gene-centric, quick overview of survival effect of a gene across all cancers, KM plots. https://precog.stanford.edu
    - Gentles, Andrew J., Aaron M. Newman, Chih Long Liu, Scott V. Bratman, Weiguo Feng, Dongkyoon Kim, Viswam S. Nair, et al. “The Prognostic Landscape of Genes and Infiltrating Immune Cells across Human Cancers.” Nature Medicine 21, no. 8 (August 2015): 938–45. https://doi.org/10.1038/nm.3909. - TCGA pan-cancer survival analysis PRECOG, CIBERSORT. 39 cancers. Intro into heterogeneity. Z-score description. Batch effect does not significantly affect z-scores. 2/3 prognostic genes shared across cancers. AutoSOME clustering method

- `GEPIA` - single- and multiple-gene analyses of TCGA data. Gene expression in different tumor-normal comparisons, differentially expressed genes, correlation analysis, similar genes, survival analysis. http://gepia.cancer-pku.cn/
    - Zefang Tang et al., “GEPIA: A Web Server for Cancer and Normal Gene Expression Profiling and Interactive Analyses,” Nucleic Acids Research 45, no. W1 (July 3, 2017): W98–102, https://doi.org/10.1093/nar/gkx247. - TCGA and GTEX web interface. Classical analyses - differential expression analysis, profiling plotting, correlation analysis, patient survival analysis, similar gene detection and dimensionality reduction analysis. http://gepia.cancer-pku.cn/
- `GEPIA2` - isoform-level TCGA analysis. Cancer subtype-specific analyses. Eight types of expression analyses, and additional Cancer Subtype Classifier and Expression Comparison. Python package for API access. http://gepia2.cancer-pku.cn
    - Tang, Zefang, Boxi Kang, Chenwei Li, Tianxiang Chen, and Zemin Zhang. “GEPIA2: An Enhanced Web Server for Large-Scale Expression Profiling and Interactive Analysis.” Nucleic Acids Research, May 22, 2019. https://doi.org/10.1093/nar/gkz430.



<!--
- `PrognoScan`, Gene-centric, survival effect of a gene in cancer studies from GEO. http://dna00.bio.kyutech.ac.jp/PrognoScan/
-->

- `UALCAN` - Gene-centric, tumor-normal expression, survival analusis, TCGA cancers. http://ualcan.path.uab.edu/
    - Chandrashekar DS, Bashel B, Balasubramanya SAH, Creighton CJ, Rodriguez IP, Chakravarthi BVSK and Varambally S. UALCAN: A portal for facilitating tumor subgroup gene expression and survival analyses. Neoplasia. 2017 Aug;19(8):649-658. doi: 10.1016/j.neo.2017.05.002 [PMID:28732212]

- `Project Betastasis` - Gene-centric, survival analysis, gene expression, select cancer studies. http://www.betastasis.com/

- `OncoLnc` - Gene-centric, survival analysis in any TCGA cancer. http://www.oncolnc.org/

### Methods to find best cutoff for survival

- `KMplotter` - the Kaplan Meier plotter is capable to assess the effect of 54,675 genes on survival using 18,674 cancer samples. These include 5,143 breast, 1,816 ovarian, 2,437 lung, 364 liver, 1,065 gastric cancer patients with relapse-free and overall survival data. The miRNA subsystems include additional 11,456 samples from 20 different cancer types. Primary purpose of the tool is a meta-analysis based biomarker assessment.
    - Györffy, Balazs, Andras Lanczky, Aron C. Eklund, Carsten Denkert, Jan Budczies, Qiyuan Li, and Zoltan Szallasi. “An Online Survival Analysis Tool to Rapidly Assess the Effect of 22,277 Genes on Breast Cancer Prognosis Using Microarray Data of 1,809 Patients.” Breast Cancer Research and Treatment 123, no. 3 (October 2010): 725–31. https://doi.org/10.1007/s10549-009-0674-9. - cutoff selection for survival by scanning gene expression range.

- `ctree` function for automatic cutoff finding and building a regression tree out of multiple covariates. `partykit::ctree()`. 
    - Hothorn, Torsten, Kurt Hornik, and Achim Zeileis. “Ctree: Conditional Inference Trees.” The Comprehensive R Archive Network, 2015, 1–34.

- `Cutoff Finder` - web tool for finding optimal dichotomization with respect to an outcome or survival variable. Five methods. http://molpath.charite.de/cutoff/
    - Budczies, Jan, Frederick Klauschen, Bruno V. Sinn, Balázs Győrffy, Wolfgang D. Schmitt, Silvia Darb-Esfahani, and Carsten Denkert. “Cutoff Finder: A Comprehensive and Straightforward Web Application Enabling Rapid Biomarker Cutoff Optimization.” PloS One 7, no. 12 (2012): e51862. https://doi.org/10.1371/journal.pone.0051862.


## Cancer driver genes

- Cancer Gene Census (CGC), download [COSMIC](http://cancer.sanger.ac.uk/cosmic/download)
    - Hudson, T. J. et al. International network of cancer genome projects. Nature 464, 993–8 (2010).
    - `data/Census_all*.csv` - [The cancer Gene Census](http://cancer.sanger.ac.uk/census)
    - `data/COSMIC_genes.txt` - Genes sorted by the number of records associated with them. Obtained using `zcat <CosmicCompleteTargetedScreensMutantExport.tsv.gz | sed '1d' | cut -f1 | sort | uniq -c | sort -k1 -r -n > COSMIC_genes.txt`
    - `data/CosmicCodingMuts.vcf.gz` - VCF file of all coding mutations in the current release (release v83, 7th November 2017).

- Tumor suppressor gene database (TSGene), https://bioinfo.uth.edu/TSGene/
    - Zhao, M., Sun, J. & Zhao, Z. TSGene: a web resource for tumor suppressor genes. Nucleic Acids Res, 41(Database issue), D970–6 (2013).
    - Download various lists of tumor suppressor genes, https://bioinfo.uth.edu/TSGene/download.cgi

- `OncoScape` - Genes with oncogenic/tumor suppressor/combined scores as a sum contribution from gene expression, somatic mutations, DNA copy-number and methylation as well as data from shRNA knock-down screens. http://oncoscape.nki.nl/
    - Schlicker, Andreas, Magali Michaut, Rubayte Rahman, and Lodewyk F. A. Wessels. “OncoScape: Exploring the Cancer Aberration Landscape by Genomic Data Fusion.” Scientific Reports 6 (20 2016): 28103. https://doi.org/10.1038/srep28103.

- `data/Bailey_2018_cancer_genes.xlsx` - Table S1, consensus list of cancer driver genes.
	- Bailey, Matthew H., Collin Tokheim, Eduard Porta-Pardo, Sohini Sengupta, Denis Bertrand, Amila Weerasinghe, Antonio Colaprico, et al. “Comprehensive Characterization of Cancer Driver Genes and Mutations.” Cell 173, no. 2 (April 5, 2018): 371-385.e18. https://doi.org/10.1016/j.cell.2018.02.060. - Pan-Cancer mutation analysis. Combined use of 26 tools (https://www.cell.com/cell/fulltext/S0092-8674(18)30237-X#secsectitle0075, description of each tool in Methods) on harmonized data. 299 cancer driver genes, >3,400 putative missense driver mutations. Table S6 - excluded TCGA samples.

- `data/TARGET_db_v3_02142015.xlsx` - TARGET (tumor alterations relevant for genomics-driven therapy) is a database of genes that, when somatically altered in cancer, are directly linked to a clinical action. TARGET genes may be predictive of response or resistance to a therapy, prognostic, and/or diagnostic. https://software.broadinstitute.org/cancer/cga/target

- `data/Tokheim_2016_cancer_driver_genes.xlsx` - Dataset S2: Predicted driver genes by various number of methods
    - Tokheim, Collin J., Nickolas Papadopoulos, Kenneth W. Kinzler, Bert Vogelstein, and Rachel Karchin. “Evaluating the Evaluation of Cancer Driver Genes.” Proceedings of the National Academy of Sciences 113, no. 50 (December 13, 2016): 14330–35. https://doi.org/10.1073/pnas.1616440113. - 20/20+ machine learning method, ratiometric approach to predict cancer driver genes. Performance comparison of other methods, 20/20+, TUSON, OncodriveFML and MutsigCV are the top performers. https://github.com/KarchinLab/2020plus

## Cancer driver mutations

- `clinvar` -  tools to convert ClinVar data into a tab-delimited flat file, and also provides that resulting tab-delimited flat file. https://github.com/macarthur-lab/clinvar

- `CANCERSIGN` - identifies 3-mer and 5-mer mutational signatures, cluster samples by signatures. Based on Alexandrov method, Non-negative matrix factorization, explanation. Other tools - SomaticSignatures, SigneR, deconstructSigs, compared in Table 1. https://github.com/ictic-bioinformatics/CANCERSIGN
    - Bayati, Masroor, Hamid Reza Rabiee, Mehrdad Mehrbod, Fatemeh Vafaee, Diako Ebrahimi, Alistair Forrest, and Hamid Alinejad-Rokny. “CANCERSIGN: A User-Friendly and Robust Tool for Identification and Classification of Mutational Signatures and Patterns in Cancer Genomes.” BioRxiv, January 1, 2019, 424960. https://doi.org/10.1101/424960.


## Drugs

- `CARE` - biomarker identification from interactions of drug target genes with other genes. Multivariate linear modeling with interaction term. Illustrative example of interaction of BRAF mutation and EGFR expression. Sample separation by gene expression correlation with CARE score better predicts survival. Comparison with correlation, elastic net, support vector regression. http://care.dfci.harvard.edu/, download page http://care.dfci.harvard.edu/download/, nls_logsig tool to compute AUC for dose curves.
    - Jiang, Peng, Winston Lee, Xujuan Li, Carl Johnson, Jun S. Liu, Myles Brown, Jon Christopher Aster, and X. Shirley Liu. “Genome-Scale Signatures of Gene Interaction from Compound Screens Predict Clinical Efficacy of Targeted Cancer Therapies.” Cell Systems 6, no. 3 (March 2018): 343-354.e5. https://doi.org/10.1016/j.cels.2018.01.009.


- `CellMinerCDB` - genomics (gene expression, mutations, copy number, methylation, and protein expression) and pharmacogenomics (drug responses and genomics interplay) analyses of cancer cell lines. Integrates NCI-60, GDSC, CCLE, CTRP, and NCI-SCLC databases built on top of `rcellminer` R package. Correlation and multivariate analyses. Tissue-specific analysis. https://discover.nci.nih.gov/cellminercdb/, 10m video tutorial https://youtu.be/XljXazRGkQ8.
    - Rajapakse, Vinodh N., Augustin Luna, Mihoko Yamade, Lisa Loman, Sudhir Varma, Margot Sunshine, Francesco Iorio, et al. “CellMinerCDB for Integrative Cross-Database Genomics and Pharmacogenomics Analyses of Cancer Cell Lines.” IScience 10 (December 2018): 247–64. https://doi.org/10.1016/j.isci.2018.11.029.

- `DSigDB` - drug-gene signature database. D1 (approved drugs), D2 (kinase inhibitors), D3 (perturbagent signatures), D4 (computational predictions). Download, online. http://tanlab.ucdenver.edu/DSigDB/DSigDBv1.0/download.html
    - Yoo, Minjae, Jimin Shin, Jihye Kim, Karen A. Ryall, Kyubum Lee, Sunwon Lee, Minji Jeon, Jaewoo Kang, and Aik Choon Tan. “DSigDB: Drug Signatures Database for Gene Set Analysis: Fig. 1.” Bioinformatics 31, no. 18 (September 15, 2015): 3069–71. https://doi.org/10.1093/bioinformatics/btv313.

- `GDA` - Genomics and Drugs integrated Analysis. The Genomics and Drugs integrated Analysis portal (GDA) is a web-based tool that combines NCI60 uniquely large number of drug sensitivity data with CCLE and NCI60 gene mutation and expression profiles. Gene-to-drug and reverse analysis. http://gda.unimore.it/

- `OncoKB` - OncoKB cancer gene database, different levels of evidence, fully downloadable. http://oncokb.org
    - Chakravarty, Debyani, Jianjiong Gao, Sarah M. Phillips, Ritika Kundra, Hongxin Zhang, Jiaojiao Wang, Julia E. Rudolph, et al. “OncoKB: A Precision Oncology Knowledge Base.” JCO Precision Oncology 2017 (July 2017).

- `CancerRxGene` - Drug-gene targets. Lots of drug sensitivity information. http://www.cancerrxgene.org/
    - Yang, Wanjuan, Jorge Soares, Patricia Greninger, Elena J. Edelman, Howard Lightfoot, Simon Forbes, Nidhi Bindal, et al. “Genomics of Drug Sensitivity in Cancer (GDSC): A Resource for Therapeutic Biomarker Discovery in Cancer Cells.” Nucleic Acids Research 41, no. Database issue (January 2013): D955-961. https://doi.org/10.1093/nar/gks1111.

- `CTRP` - The Cancer Therapeutics Response Portal (CTRP) links genetic, lineage, and other cellular features of cancer cell lines to small-molecule sensitivity with the goal of accelerating discovery of patient-matched cancer therapeutics. https://portals.broadinstitute.org/ctrp/

- Drug combination screen, synergy. Statistics for the analysis of large-scale drug screens, 108 drugs, 40 cell lines. Bliss independence model description. Bliss-based linear model to evaluate viabilities for individual drugs. Web-interface: http://www.cmtlab.org:3000/combo_app.html. Code to reproduce the analysis: https://github.com/arnaudmgh/synergy-screen. Raw data: https://raw.githubusercontent.com/arnaudmgh/synergy-screen/master/data/rawscreen.csv
    - Amzallag, Arnaud, Sridhar Ramaswamy, and Cyril H. Benes. “Statistical Assessment and Visualization of Synergies for Large-Scale Sparse Drug Combination Datasets.” BMC Bioinformatics 20, no. 1 (December 2019). https://doi.org/10.1186/s12859-019-2642-7.



## Data

- `UCSCXenaTools` - An R package downloading and exploring data from UCSC Xena data hubs. CRAN: https://cran.r-project.org/web/packages/UCSCXenaTools/, GitHub: https://github.com/ShixiangWang/UCSCXenaTools, https://shixiangwang.github.io/UCSCXenaTools/

- BREAST CANCER LANDSCAPE RESOURCE, A web portal to proteomics, transcriptomics, genomics and metabolomics of breast cancer. Downloada http://www.breastcancerlandscape.org/
    - Consortia Oslo Breast Cancer Research Consortium (OSBREAC), Henrik J. Johansson, Fabio Socciarelli, Nathaniel M. Vacanti, Mads H. Haugen, Yafeng Zhu, Ioannis Siavelis, et al. “Breast Cancer Quantitative Proteome and Proteogenomic Landscape.” Nature Communications 10, no. 1 (December 2019): 1600. https://doi.org/10.1038/s41467-019-09018-y. - Proteogenomics of breast cancer subtypes. ~10K proteins by LS-MS/MS. 9 samples for each of the five PAM50 subtypes. Protein expression partially recapitulates PAM50 subtypes, their own consensus clustering. High correlation with mRNA, less so for CNV. Correlation of 290 proteins that are FDA-approved drug targets. Online tool, http://www.breastcancerlandscape.org/, supplementary Data 1 has the full protein expression matrix,https://www.nature.com/articles/s41467-019-09018-y#Sec15

- `Refine.bio` harmonizes petabytes of publicly available biological data into ready-to-use datasets for cancer researchers and AI/ML scientists. https://www.refine.bio/. Documentation, http://docs.refine.bio/en/latest/, GitHub, https://github.com/AlexsLemonade/refinebio.

- Zehir, Ahmet, Ryma Benayed, Ronak H Shah, Aijazuddin Syed, Sumit Middha, Hyunjae R Kim, Preethi Srinivasan, et al. “Mutational Landscape of Metastatic Cancer Revealed from Prospective Clinical Sequencing of 10,000 Patients.” Nature Medicine 23, no. 6 (May 8, 2017): 703–13. https://doi.org/10.1038/nm.4333. - MSK-IMPACT study. Deep sequencing of 341-410 genes in 10,000 samples in multiple cancers. Focus on mutations, copy number alterations, fusions. Data at http://www.cbioportal.org/study?id=msk_impact_2017#summary, downloadable, includes clinical data for survival analysis.

- Gendoo, Deena M.A., Michael Zon, Vandana Sandhu, Venkata Manem, Natchar Ratanasirigulchai, Gregory M. Chen, Levi Waldron, and Benjamin Haibe-Kains. “MetaGxData: Clinically Annotated Breast, Ovarian and Pancreatic Cancer Datasets and Their Use in Generating a Multi-Cancer Gene Signature,” November 12, 2018. https://doi.org/10.1101/052910. - MetaGxData package containing breast and ovarian cancer data, microarray- and RNA-seq gene expression and clinical annotations. Scripts to conduct genome-wide survival analysis for all genes. https://github.com/bhklab/MetaGxData 

- `DepMap` - Large-scale RNAi screen for cancer vulnerability genes in 501 cell lines from 20 cancers, shRNA silencing ~17,000 genes. DEMETER - Modeling and removal of shRNA off-target effects. 6 sigma cutoff of DEMETER scores to identify 769 differential gene dependencies. ATLANTIS model to predict other genes - MDPs, marker dependency pairs. Main data portal: https://depmap.org/portal/download/
    - Tsherniak, Aviad, Francisca Vazquez, Phil G. Montgomery, Barbara A. Weir, Gregory Kryukov, Glenn S. Cowley, Stanley Gill, et al. “Defining a Cancer Dependency Map.” Cell 170, no. 3 (July 2017): 564-576.e16. https://doi.org/10.1016/j.cell.2017.06.010. [Supplemental tables](https://www.sciencedirect.com/science/article/pii/S0092867417306517?via%3Dihub#app2), `DepMap_TableS3_DependencyCorrelation.csv` - Table S3. Gene Dependency-Dependency Correlations, pairs of genes essential for proliferation/viability. Columns: Gene symbol 1, Gene symbol 2, correlation (r), z_score. [Source](https://ars.els-cdn.com/content/image/1-s2.0-S0092867417306517-mmc3.csv)

- `CCLE2 data` - CCLE characterization using sequencing technologies. Data described: RNA splicing, DNA methylation, Histone modification, miRNA expression, RPPA for 1072 cells. Data availability: https://portals.broadinstitute.org/ccle/data, https://depmap.org/portal/download/
    - Ghandi, Mahmoud, Franklin W. Huang, Judit Jané-Valbuena, Gregory V. Kryukov, Christopher C. Lo, E. Robert McDonald, Jordi Barretina, et al. “Next-Generation Characterization of the Cancer Cell Line Encyclopedia.” Nature, May 8, 2019. https://doi.org/10.1038/s41586-019-1186-3.


### TCGA PanCancer

- ATAC-seq data in 410 tumor samples from TCGA (23 cancer types). Correlation with gene expression predicts distal interactions. 18 clusters by cancer type. Data: hg19 coordinates of pan-cancer and BRCA-specific ATAC-seq peaks (Data S2), eQTLs (Data S5), peak-to-gene and enhancer-to-gene links (Data S7), and more https://gdc.cancer.gov/about-data/publications/ATACseq-AWG 
    - Corces, M. Ryan, Jeffrey M. Granja, Shadi Shams, Bryan H. Louie, Jose A. Seoane, Wanding Zhou, Tiago C. Silva, et al. “The Chromatin Accessibility Landscape of Primary Human Cancers.” Edited by Rehan Akbani, Christopher C. Benz, Evan A. Boyle, Bradley M. Broom, Andrew D. Cherniack, Brian Craft, John A. Demchok, et al. Science 362, no. 6413 (2018). https://doi.org/10.1126/science.aav1898.

- Papers and supplementary data from PanCancer publications. Clinical annotations, RNA-seq counts, RPPA, Methylation, miRNA, copy number, mutations in .maf format. https://gdc.cancer.gov/about-data/publications/pancanatlas
    - Ding, Li, Matthew H. Bailey, Eduard Porta-Pardo, Vesteinn Thorsson, Antonio Colaprico, Denis Bertrand, David L. Gibbs, et al. “Perspective on Oncogenic Processes at the End of the Beginning of Cancer Genomics.” Cell 173, no. 2 (April 5, 2018): 305-320.e10. https://doi.org/10.1016/j.cell.2018.03.033. - An overview of PanCancer Atlas.

- The Pan-Cancer analysis by TCGA consortium, all papers. https://www.cell.com/pb-assets/consortium/pancanceratlas/pancani3/index.html

- TCGA MC3 variant calling project. Eight variant callers. Protocols for filtering samples, variants. Public and controlled access MAF files at https://gdc.cancer.gov/about-data/publications/mc3-2017
    - Ellrott, Kyle, Matthew H. Bailey, Gordon Saksena, Kyle R. Covington, Cyriac Kandoth, Chip Stewart, Julian Hess, et al. “Scalable Open Science Approach for Mutation Calling of Tumor Exomes Using Multiple Genomic Pipelines.” Cell Systems 6, no. 3 (March 2018): 271-281.e7. https://doi.org/10.1016/j.cels.2018.03.002.

- `PCAGW` - The PCAWG study is an international collaboration to identify common patterns of mutation in more than 2,800 cancer whole genomes from the International Cancer Genome Consortium. The project produced large amount data with many types including simple somatic mutations (SNVs, MNVs and small INDELs), large-scale somatic structural variations, copy number alterations, germline variations, RNA expression profiles, gene fusions, and phenotypic annotations etc. PCAWG data have been imported, processed and made available in the following four major online resources for download and exploration by the cancer researchers worldwide. http://docs.icgc.org/pcawg/
    - Goldman, Mary, Junjun Zhang, Nuno A. Fonseca, Qian Xiang, Brian Craft, Elena Piñeiro, Brian O’Connor, et al. “Online Resources for PCAWG Data Exploration, Visualization, and Discovery.” BioRxiv, October 18, 2017. https://doi.org/10.1101/163907. https://www.biorxiv.org/content/early/2017/10/18/163907


## Methylation

- `MEXPRESS` - Gene-centric methylation and correlation with clinical parameters. http://mexpress.be/

- `Pancan-meQTL` database of meQTLs across 23 TCGA cancer types. Cis-, trans-meQTLs, pancancer-meQTLs, survival meQTLs. SNP-, gene-, CpG-centric search for each cancer. Visualization, KM plots for survival. Download. http://bioinfo.life.hust.edu.cn/Pancan-meQTL/
    - Gong, Jing, Hao Wan, Shufang Mei, Hang Ruan, Zhao Zhang, Chunjie Liu, An-Yuan Guo, Lixia Diao, Xiaoping Miao, and Leng Han. “Pancan-MeQTL: A Database to Systematically Evaluate the Effects of Genetic Variants on Methylation in Human Cancer.” Nucleic Acids Research, September 7, 2018. https://doi.org/10.1093/nar/gky814.


## Misc

-  SMAP is a pipeline for the process of xenografts sequencing data. It takes FASTQ as input and outputs specie-specific BAM or gene counts. https://github.com/cit-bioinfo/SMAP

