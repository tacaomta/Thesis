---
layout: thesis-cover
---

<template #network>
  <ThesisNetwork />
</template>
---
layout: default
title: From Better Inference to Better Data
eyebrow: THESIS OVERVIEW
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
eyebrow: WHY DOES IT MATTER?
---

<RegulatoryGenes />
---
layout: default
title: What Data Do We Observe?
eyebrow: EXPERIMENTAL DATA
---

<ObservedData />
---
layout: default
title: Why is Time-series GRN Inference Difficult?
eyebrow: CHALLENGES
---

<TimeSeriesDifficulty />
<!--
Time-series data provide dynamic information, but reconstructing the
                underlying regulatory network remains challenging.
-->
---
layout: default
title: What are common GRN Inference Approaches?
eyebrow: INFERENCE METHODS
---

<CommonMethods />
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
title: What Do We Want to Improve?
eyebrow: MOTIVATION
---

<Pipeline01 />
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
title: What is the experimental framwork?
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
<!--
First, MIFS constructs the candidate regulator set. However, MIFS is based on an approximate dependency measure and may not identify the optimal set. Therefore, we introduce the SWAP routine to iteratively refine this set.
-->
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

<!-- CHAPTER 3 -->
<!--“In the first publication, I focused on the inference method. By introducing multiple-level discretization, we can preserve more information from gene expression dynamics than a purely Boolean representation.
However, when moving toward machine learning, another question arises: how should a regulatory relationship be represented so that a learning model can actually learn from it? -->
---
layout: default
title: How Do We Represent Regulatory Relationships for Machine Learning?
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
title: Does the framework outperform traditional GRN inference methods on biological data?
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
<!--From a computational standpoint, training on small networks saves 15% to 25% in training time compared to large-scale training. Furthermore, while traditional methods have to re-compute everything from scratch for every new dataset, our pre-trained classifiers run online inference in a fraction of a second.-->
---
layout: default
title: What are the operational requirements and scope of applicability?
eyebrow: LIMITATION & DEVELOPMENT
---
<LimitationDevelopment />