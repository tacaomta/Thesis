---
title: "GRN Inference — PhD Thesis"
titleTemplate: "%s"
layout: thesis-cover
---

<template #network>
  <ThesisNetwork />
</template>


---
layout: default
title: "From Better Inference to Better Data"
eyebrow: "THESIS OVERVIEW"
---

<ThesisOverview />

---
layout: default
title: What is a Gene Regulatory Network?
eyebrow: GENE REGULATORY NETWORK
---

<GRNs />

---
layout: default
title: What are we actually Trying to Infer?
eyebrow: RESEARCH PROBLEM
---

<InferenceProblem />

---
layout: default
title: Why do Regulatory Genes Matter?
eyebrow: SIGNIFICANCE
---

<RegulatoryGenes />

---
layout: default
title: Why is Time-series GRN Inference Difficult?
eyebrow: CHALLENGES
---
<TimeSeriesDifficulty /> 
---
layout: default
title: Where Does This Thesis Fit?
eyebrow: RESEARCH SCOPE
---

<GRNWorkFlow />

---
layout: default
title: What Have We Done to Improve?
eyebrow: RESEARCH GAPS
---

<ResearchGaps />

---
layout: default
title: How is gene expression commonly represented for GRN inference?
eyebrow: EXISTING APPROACHES
---

<ExistingApproaches />


---
layout: default
title: What Do We Want to Improve?
eyebrow: MOTIVATION
---

<Motivations />


---
layout: default
title: How Does the Discretization Network Model Represent Gene Dynamics?
eyebrow: DISCRETIZATION NETWORK MODEL
---

<DiscretizationNetworkModel />

---
layout: default
title: How Do We Evaluate an Inferred Network?
eyebrow: PERFORMANCE EVALUATION
---

<NetworkInference />

---
layout: default
title: What is the experimental framework?
eyebrow: METHODOLOGY
---

<Methodology />

---
layout: default
title: How Do We Determine the Optimal Discretization Level?
eyebrow: DISCRETIZATION
---

<Discretization />

---
layout: default
title: How Are Potential Regulators Selected and Refined?
eyebrow: FEATURE SELECTION
---

<FeatureSelectionStage />

---
layout: default
title: Which Datasets Are Used for Evaluation?
eyebrow: DATASETS
---

<Datasets01 />

---
layout: default
title: How Does Three-Level Proportion Vary?
eyebrow: THREE-LEVEL PROPORTION
---

<Proportion />

---
layout: default
title: Does the Proposed Method Perform Well across All Metrics?
eyebrow: RESULTS - ARTIFICIAL DATASET
---

<ArtificialResults />

---
layout: default
title: How Does Network Complexity Affect Inference Performance?
eyebrow: RESULTS - ARTIFICIAL DATASET
---

<IncomingLinksResults />

---
layout: default
title: How Well Does the Inferred Network Recover the True Structure?
eyebrow: RESULTS - ECOLI DATASET
---

<StructuralAccuracy />

---
layout: default
title: How Well Does the Model Explain the Underlying Mechanism?
eyebrow: RESULTS - ECOLI DATASET
---

<DynamicsAccuracy />

---
layout: default
title: How Does Computational Efficiency Vary Across Methods?
eyebrow: RUNNING TIME
---

<RunningTime />

---
layout: default
title: What Have We Achieved, and What Remains to Be Improved?
eyebrow: CONCLUSION
---

<Conclusion />

---
layout: default
title: Why do existing machine learning frameworks still fail to generalize?
eyebrow: RESEARCH GAP 02
---

<RepresentationMotivations />

---
layout: default
title: How did we build a learning framework for GRN inference?
eyebrow: PROPOSED FRAMEWORK
---
<LearningFramework />

---
layout: default
title: How is gene profile reformulated into a binary classification task?
eyebrow: DATA REPRESENTATION
---
<DataRepresentation />

---
layout: default
title: What unique advantages does the unified representation offer?
eyebrow: METHODOLOGICAL HIGTLIGHTS
---
<MethodAdvantages />

---
layout: default
title: How were the datasets and evaluation metrics configured?
eyebrow: EXPERIMENTAL SETUP
---
<ExperimentalSetup />

---
layout: default
title: How did models perform on scale-free topological networks?
eyebrow: RESULTS - TOPOLOGICAL NETWORKS
---
<AUPRToys />

---
layout: default
title: How Does the Performance on Biological Data?
eyebrow: RESULTS - BIOLOGICAL NETWORKS
---
<AUPREcoli />

---
layout: default
title: Can models trained on small networks effectively infer large-scale GRNs?
eyebrow: RESULTS - KEY FINDINGS
---
<KeyFindings />

---
layout: default
title: Can the Model Maintain Its Performance with Fewer Time Steps?
eyebrow: RESULTS - KEY FINDINGS
---
<TimeStepVariation />

---
layout: default
title: What are the computational cost advantages of small-network training?
eyebrow: COMPUTATIONAL PERFORMANCE
---
<ComputationalComparison />

---
layout: default
title: What are the operational requirements and scope of applicability?
eyebrow: LIMITATION & DEVELOPMENT
---
<LimitationDevelopment />

---
layout: default
title: What are the main contributions of this representation learning framework?
eyebrow: CONCLUSION
---
<LearningConclusion />

---
layout: default
title:  Why is time-series data scarcity a critical bottleneck in GRN inference?
eyebrow: RESEARCH GAP 03
---
<ResearchGap03 />

---
layout: default
title:  Why do conventional data augmentation methods struggle with sparse transcriptomic data?
eyebrow: LIMITATIONS OF EXISTING METHODS
---
<LimitationsExistingMethods />

---
layout: default
title:  Can an Autoencoder framework synthesize realistic time-series expression data to restore GRN inference accuracy?
eyebrow: RESEARCH GOALS & HYPOTHESIS
---
<ResearchGoals />

---
layout: default
title:  How is the end-to-end Synthetic-MIDNI framework structured?
eyebrow: ARCHITECHTURAL OVERVIEW
---
<SyntheticFramework />

---
layout: default
title:  How does pairwise temporal vector concatenation preserve transition dynamics?
eyebrow: FEATURE ENGINEERING
---
<FeatureEngineering />

---
layout: default
title:   How does the model perform iterative auto-regressive time-series synthesis?
eyebrow: GENERATIVE MECHANISM
---
<GenerativeMechanism />

---
layout: default
title:   How Was the Experimental Setup Designed?
eyebrow: EXPERIMENTAL SETUP
---
<ExperimentalSetup04 />

---
layout: default
title:  Which Metrics Are Used to Evaluate GRN Inference?
eyebrow: EVALUATION METRICS
---
<EvaluationMetrics />

---
layout: default
title:  How well performance gains on ternary datasets?
eyebrow: RESULTS - TERNARY DATASETS
---
<TernaryDatasetsRecovery />

---
layout: default
title:  How well performance gains on Boolean datasets?
eyebrow: RESULTS - BOOLEAN DATASETS
---
<BooleanDatasetsRecovery />

---
layout: default
title: How Well Is Dynamic Fidelity Preserved?
eyebrow: RESULTS - DYNAMICS FIDELITY
---
<DynamicsFidelity />

---
layout: default
title: How Diverse Are the Synthesized Expression Profiles?
eyebrow: RESULTS - DATA DIVERSITY ANALYSIS
---
<DataDiversity />

---
layout: default
title: What are Key Findings and Biological Significance?
eyebrow: SUMMARY AND IMPLICATIONS
---
<SummaryOfCoreFindings />

---
layout: default
title: Where Can This Research Go Next?
eyebrow: FUTURE HORIZONS
---
<FutureHorizons />

---
layout: default
title: What Have We Achieved?
eyebrow: THESIS SYMMARY
---
<ThesisSummary />

---
layout: default
title: Who Made This Journey Possible?
eyebrow: ACKNOWLEDGEMENT
---
<Acknowledgement />

---
layout: default
title:
eyebrow: QAs 
---
<QAs />
---
layout: default
title: How do GRNs look like?
eyebrow: GRNs 
---
<GRNExample />
---
layout: default
title: How does MIFS select candidate regulators?
eyebrow: MIDNI
---
<MIFSS />
---
layout: default
title: How does SWAP refine?
eyebrow: MIDNI
---
<SWAP />
---
layout: default
title: Synthetic network simulation
eyebrow: SITTF
---
<BAmodels />
---
layout: default
title: Classifier Hyperparameters
eyebrow: SITTF
---
<ArgsModels />
---
layout: default
title: Topological Dataset Symmary
eyebrow: SITTF
---
<TopologicalDatasetTable />
---
layout: default
title: E.coli Dataset Symmary
eyebrow: SITTF
---
<EcoliTable />
---
layout: default
title: Detail Performance on E.coli Datasets
eyebrow: SITTF
---
<EcoliDetails10 />
---
layout: default
title: Detail Performance on E.coli Datasets
eyebrow: SITTF
---
<EcoliDetails50 />
---
layout: default
title: Detail Performance on E.coli Datasets
eyebrow: SITTF
---
<EcoliDetails100 />
---
layout: default
title: Effect of Training Set Size on AUPR
eyebrow: SITTF
---
<EcoliScale />
---
layout: default
title:   What is the design and parameter configuration of the generative Autoencoder?
eyebrow: AUTOENCODER ARCHITECTURE
---
<DeepLearningArchitecture />

