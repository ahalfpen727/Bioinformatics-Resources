# awesome-multi-omics

List of software packages for multi-omics data analysis. A
shameless copy of Sean Davis'
[awesome-single-cell](https://github.com/seandavi/awesome-single-cell)
repo.

[Contributions welcome](https://github.com/mikelove/awesome-multi-omics/blob/master/CONTRIBUTING.md)...

For brevity, below lists only the first author of multi-omics methods.

## Software packages and methods

### Multi-omics correlation or factor analysis

- 2007 - **SCCA** - Parkhomenko - sparse CCA - [paper 1](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2367499/), [paper 2](https://doi.org/10.2202/1544-6115.1406) 
- 2008 - **PCCA** - Waaijenborg - penalized CCA / CCA-EN - [paper](https://doi.org/10.2202/1544-6115.1329)
- 2009 - [PMA](https://CRAN.r-project.org/package=PMA) - Witten - Sparse Multi CCA - [paper 1](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2697346/), [paper 2](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2861323/)
- 2009 - **sPLS** - Lê Cao - sparse PLS - [paper](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2640358/)
- 2009 - [gesca](https://CRAN.r-project.org/package=gesca) - Hwang - RGSCA regularized generalized structured component analysis - [paper](https://doi.org/10.1007/s11336-009-9119-y) 
- 2010 - **Regularized dual CCA** - Soneson - [paper](https://doi.org/10.1186/1471-2105-11-191)
- 2011 - [RGCCA](https://cran.r-project.org/package=RGCCA) - Tenenhaus - Regularized Generalized CCA and Sparse Generalized CCA - [paper 1](https://www.ncbi.nlm.nih.gov/pubmed/28536930), [paper 2](https://www.ncbi.nlm.nih.gov/pubmed/24550197)
- 2011 - **SNMNMF** - Zhang - Sparse Network-regularized Multiple Non-negative Matrix Factorization - [paper](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3117336/)
- 2012 - [STATIS/DiSTATIS](https://github.com/HerveAbdi/DistatisR) - Abdi - structuring three-way statistical tables - [paper](https://doi.org/10.1002/wics.198)
- 2012 - **joint NMF** - Zhang - extension of NMF to multiple datasets - [paper](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3479191/)
- 2012 - **sMBPLS** - Li - sparse MultiBlock Partial Least Squares - [paper](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3463121/)
- 2012 - **Bayesian group factor analysis** - Virtanen - [paper](http://proceedings.mlr.press/v22/virtanen12.html)
- 2012 - [RIMBANET](http://research.mssm.edu/integrative-network-biology/RIMBANET/RIMBANET_overview.html) - Zhu - Reconstructing Integrative Molecular Bayesian Networks - [paper](https://doi.org/10.1371/journal.pbio.1001301)
- 2013 - [FactoMineR](https://cran.r-project.org/package=FactoMineR) - Abdi - MFA: multiple factor analysis - [paper](https://doi.org/10.1002/wics.1246)
- 2013 - [JIVE](https://genome.unc.edu/jive/) - Lock - joint & individual variance explained - [paper](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3671601/)
- 2013 - [PANDA](https://bioconductor.org/packages/release/bioc/html/pandaR.html) - Glass - Passing Attributes between Networks for Data Assimilation
- 2014 - [omicade4](https://bioconductor.org/packages/omicade4) - Meng - MCIA: multiple co-interia analysis - [paper](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4053266/)
- 2014 - [STATegRa](https://bioconductor.org/packages/STATegRa) - Gomez-Cabrero - DISCO, JIVE, & O2PLS (several papers)
- 2014 - **Joint factor model** - Ray - [paper](https://doi.org/10.1093/bioinformatics/btu064)
- 2014 - [GFAsparse](https://research.cs.aalto.fi/pml/software/GFAsparse/) - Khan - group factor analysis sparse [paper 1](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4147909/), [paper 2](https://doi.org/10.1093/bioinformatics/btw207)
- 2015 - [CCAGFA](https://cran.r-project.org/package=CCAGFA) - Klami - Bayesian Canonical Correlation Analysis and Group Factor Analysis - [paper 1](https://doi.org/10.1109/TNNLS.2014.2376974), [paper 2](http://www.jmlr.org/papers/v18/16-509.html)
- 2016 - [CMF](https://cran.r-project.org/package=CMF) - Klami - collective matrix factorization
- 2016 - [moGSA](https://bioconductor.org/packages/mogsa) - Meng - multi-omics gene set analysis - [paper](https://doi.org/10.1101/046904)
- 2016 - [iNMF](https://github.com/yangzi4/iNMF) - Yang - integrative NMF - [paper](https://www.ncbi.nlm.nih.gov/pmc/articles/pmid/26377073/)
- 2016 - [BASS](https://github.com/judyboon/BASS) - Zhao - Bayesian group factor analysis - [paper](https://arxiv.org/abs/1411.2698)
- 2017 - [mixOmics](https://bioconductor.org/packages/mixOmics)
    - 2017 - Rohart - various methods - [paper](https://doi.org/10.1371/journal.pcbi.1005752)
    - 2019 - Singh - DIABLO: Data Integration Analysis for Biomarker discovery using Latent cOmponents - [paper](https://doi.org/10.1093/bioinformatics/bty1054)
- 2017 - [mixedCCA](https://github.com/irinagain/mixedCCA) - Gaynanova - sparse CCA for data of mixed types - [paper](https://arxiv.org/abs/1807.05274)
- 2017 - [SLIDE](https://github.com/irinagain/SLIDE_Rpackage) - Gaynanova - Structural Learning and Integrative Decomposition of Multi-View Data - [paper](https://arxiv.org/abs/1707.06573)
- 2017 - [fCCAC](https://github.com/pmb59/fCCAC/) - Madrigal - functional canonical correlation analysis to evaluate covariance - [paper](https://doi.org/10.1093/bioinformatics/btw724)
- 2017 - [TSKCCA](https://github.com/kosyoshida/TSKCCA) - Yoshida - Sparse kernel canonical correlation analysis - [paper](https://doi.org/10.1186/s12859-017-1543-x)
- 2017 - **SMSMA** - Kawaguchi - Supervised multiblock sparse multivariable analysis - [paper](https://doi.org/10.1093/biostatistics/kxx011)
- 2018 - [AJIVE](https://github.com/idc9/r_jive) - Feng - angle-based JIVE - [paper](https://arxiv.org/abs/1704.02060)
- 2018 - [MOFA](https://github.com/bioFAM/MOFA) - Argelaguet - multi-omics factor analysis - [paper](https://doi.org/10.15252/msb.20178124), [application](https://doi.org/10.1101/519207)
- 2018 - [PCA+CCA](https://github.com/pachterlab/PCACCA/) - Brown - [paper](https://doi.org/10.1371/journal.pgen.1007841)
- 2018 - [maui](https://github.com/BIMSBbioinfo/maui) - Ronen - multi-omics autoencoder integration - [paper](https://doi.org/10.1101/464743)
- 2018 - [JACA](https://github.com/Pennisetum/JACA) - Zhang - Joint Association and Classification Analysis - [paper](https://arxiv.org/abs/1811.08511)
- 2018 - **iPCA** - Tang - Integrated Principal Components Analysis - [paper](https://arxiv.org/abs/1810.00832)
- 2018 - [pCIA](https://www.med.upenn.edu/long-lab/software.html) - Min - penalized COI - [paper](https://www.ncbi.nlm.nih.gov/pubmed/30165424)
- 2018 - **sSCCA** - Safo - structured sparse CCA - [paper](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5677597/)

### Ecology multi-table literature

- 1994 - **COI** - Doledec - Co‐inertia analysis - [paper](https://doi.org/10.1111/j.1365-2427.1994.tb01741.x)
- 2007 - [ade4](https://CRAN.r-project.org/package=ade4) - Dray - Implementing the Duality Diagram for Ecologists - [paper](http://dx.doi.org/10.18637/jss.v022.i04)

### Chemometrics multi-table literature

- 1987 - Wold - Multi‐way principal components‐and PLS‐analysis - [paper](https://doi.org/10.1002/cem.1180010107)
- 1996 - Wold - Hierarchical multiblock PLS - [paper](https://doi.org/10.1002/(SICI)1099-128X(199609)10:5/6%3C463::AID-CEM445%3E3.0.CO;2-L)
- 2003 - Trygg - O2‐PLS, a two‐block (X–Y) latent variable regression (LVR) - [paper](https://doi.org/10.1002/cem.775)
- 2011 - Hanafi - Connections between multiple COI and consensus PCA - [paper](https://doi.org/10.1016/j.chemolab.2010.05.010)
- 2015 - [THEME](https://github.com/ThomData/R_THEME) - Verron - THEmatic Model Exploration - [paper](https://doi.org/10.1002/cem.2759)

### Behavioral research multi-table literature

- 2013 - Schouteden - DISCO SCA - distinctive and common components with simultaneous-component analysis- [paper 1](https://www.ncbi.nlm.nih.gov/pubmed/23361416), [paper 2](https://www.ncbi.nlm.nih.gov/pubmed/24178130)

### Multi-omics clustering / classification / prediction

*Note: I think that prediction of genomic tracks, e.g. ChIP-seq, from other genomic tracks is a large area of research that may deserve a separate repository. Below are methods for clustering / classification of samples into sub-types or prediction of outcomes.*

- 2009 - [iCluster](https://cran.r-project.org/package=iCluster) - Shen - [paper](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2800366/)
- 2013 - [iClusterPlus](https://bioconductor.org/packages/iClusterPlus) - Mo - [paper](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3600490/)
- 2013 - [BCC](https://github.com/ttriche/bayesCC) - Lock - Bayesian consensus clustering - [paper](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3789539/)
- 2013 - **iBAG** - Wang - Integrative Bayesian Analysis of Genomics - [paper](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3546799/)
- 2014 - [SNF](http://compbio.cs.toronto.edu/SNF/SNF/Software.html) - Wang - [paper](https://www.ncbi.nlm.nih.gov/pubmed/24464287)
- 2019 - [IBOOST](http://dlin.web.unc.edu/software/iboost/) - Wong - [paper](https://doi.org/10.1186/s13059-019-1640-4)

### Single cell multi-omics

- 2018 - [cardelino](https://github.com/PMBio/cardelino) - gene expression states to clones (SNVs from scRNA-seq + bulk exome data)
- 2018 - [clonealign](https://github.com/kieranrcampbell/clonealign) - gene expression states to clones (scRNA-seq + scDNA-seq (CNV)) - [paper](https://doi.org/10.1101/344309)

### Multi-study correlation or factor analysis

- 2016 - [MSFA](https://github.com/rdevito/MSFA) - De Vito - multi-study factor analysis: same features, different samples - [paper](https://arxiv.org/abs/1611.06350)

## Multi-omics reviews / evaluations

- 2014 - Kohl - [A practical data processing workflow for multi-OMICS projects](https://doi.org/10.1016/j.bbapap.2013.02.029)
- 2016 - Ebrahim - [Multi-omic data integration enables discovery of hidden biological regularities](https://doi.org/10.1038/ncomms13091)
- 2016 - Meng - [Dimension reduction techniques for the integrative analysis of multi-omics data](https://doi.org/10.1093/bib/bbv108)
- 2017 - Huang - [More Is Better: Recent Progress in Multi-Omics Data Integration Methods](https://doi.org/10.3389/fgene.2017.00084)
- 2017 - Hasin - [Multi-omics approaches to disease](https://doi.org/10.1186/s13059-017-1215-1)
- 2017 - Allen - [Statistical data integration: Challenges and opportunities](http://www.stat.rice.edu/~gallen/gallen_data_integration_2017.pdf)
- 2018 - McCabe - [MOVIE: Multi-Omics VIsualization of Estimated contributions](https://doi.org/10.1101/379115) - [code](https://github.com/mccabes292/movie)
- 2018 - Rappoport - [Multi-omic and multi-view clustering algorithms: review and cancer benchmark](https://doi.org/10.1093/nar/gky889)
- 2018 - Bougeard - [Current multiblock methods: Competition or complementarity? A comparative study in a unified framework](https://doi.org/10.1016/j.chemolab.2018.09.003)

## Multi-omics application papers

- 2007 - Fagan - [A multivariate analysis approach to the integration of proteomic and gene expression data](https://doi.org/10.1002/pmic.200600898)
- 2014 - Tomescu - [Integrative omics analysis. A study based on Plasmodium falciparum mRNA and protein data](https://doi.org/10.1186/1752-0509-8-S2-S4)
- 2014 - Costello (NCI/DREAM) - [A community effort to assess and improve drug sensitivity prediction algorithms](https://doi.org/10.1038/nbt.2877)
- 2016 - Wan - [TCGA2STAT: simple TCGA data access for integrated statistical analysis in R](https://doi.org/10.1093/bioinformatics/btv677) - [R notebook](http://www.liuzlab.org/TCGA2STAT/)
- 2017 - Butler - [Integrating single-cell transcriptomic data across different conditions, technologies, and species.](https://www.biorxiv.org/content/10.1101/164889v1)
- 2018 - Skelly - [Reference trait analysis reveals correlations between gene expression and quantitative traits in disjoint samples](https://www.biorxiv.org/content/10.1101/489542v1) - [R notebook](https://daskelly.github.io/reference_traits/reference_trait_analysis_walkthrough.html)
- 2018 - Stuart - [Comprehensive integration of single cell data](https://www.biorxiv.org/content/10.1101/460147v1)

## Multi-omics data management

- 2017 - [MultiAssayExperiment](https://bioconductor.org/packages/MultiAssayExperiment/) - Software for the integration of multi-omics experiments in Bioconductor - [paper](https://doi.org/10.1158/0008-5472.CAN-17-0344).
