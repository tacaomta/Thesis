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
<!--To solve these limitations, we reframe the entire problem. Instead of predicting the whole network at once, we transform GRN inference into a pairwise binary classification task. For any candidate gene pair, we simply concatenate their expression time-series profiles into a single fixed-length vector and pair it with a binary interaction label.-->
---
layout: default
title: What unique advantages does the unified representation offer?
eyebrow: METHODOLOGICAL HIGTLIGHTS
---
<MethodAdvantages />
<!--What makes this representation so effective? First, it’s completely assumption-free—the model learns temporal dependencies implicitly without manual time-lag tuning. Second, it encodes structure and time dynamics together. And most importantly, because feature length depends only on time steps $T$ rather than gene count, it creates a scale-invariant feature space.-->
---
layout: default
title: How were the datasets and evaluation metrics configured?
eyebrow: EXPERIMENTAL SETUP
---
<ExperimentalSetup />
<!--Moving on to our experimental setup, we evaluated the framework on two benchmarks: synthetic scale-free Barabási–Albert networks and realistic E. coli networks from GeneNetWeaver. Because true interactions are extremely sparse in biological systems, we chose AUPR as our primary evaluation metric over ROC.-->
---
layout: default
title: How did models perform on scale-free topological networks?
eyebrow: RESULTS - TOPOLOGICAL NETWORKS
---
<AUPRToys />
<!--On the synthetic topological datasets, every single machine learning model outperformed the random baseline. Random Forest delivered the highest overall accuracy across all network sizes. Interestingly, Gaussian Naive Bayes was the only model whose performance actually improved as network size grew, thanks to its strong probabilistic inductive bias-->
---
layout: default
title: Does the framework outperform traditional GRN inference methods on biological data?
eyebrow: RESULTS - BIOLOGICAL NETWORKS
---
<AUPREcoli />
<!--When tested on biological E. coli networks, the performance gap expanded even further. The supervised learning models achieved dramatically higher AUPR scores than traditional algorithms like Jump3 or Inferelator. GNB consistently emerged as the most reliable model across all network dimensions.-->
---
layout: default
title: Can models trained on small networks effectively infer large-scale GRNs?
eyebrow: RESULTS - KEY FINDINGS
---
<KeyFindings />
<!--Now, let's highlight our key discovery: scale invariance. A GNB model trained exclusively on small 10-gene networks achieved an AUPR of 0.373 on 50-gene networks and 0.333 on 100-gene networks. This actually matches or beats models trained directly on large networks, proving that interaction-level knowledge transfers seamlessly across scales.-->
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
<!--To be realistic about deployment, there is one key operational constraint: the test time-series length must match or exceed the training length $T$. For shorter profiles, temporal extension techniques are required. Nevertheless, the representation has proven remarkably robust across both discrete and continuous data types.-->
---
layout: default
title: What are the main contributions of this representation learning framework?
eyebrow: CONCLUSION
---
<LearningConclusion />
<!--To conclude, this work introduces a novel, scale-invariant representation that reformulates GRN inference into a binary classification problem. By removing time-lag heuristics and enabling cross-network data transfer, it effectively overcomes class imbalance and offers a highly scalable tool for systems biology. Thank you for your attention!-->
---
layout: default
title:  Why is time-series data scarcity a critical bottleneck in GRN inference?
eyebrow: RESEARCH GAP 03
---
<ResearchGap03 />
<!--Welcome everyone. To kick off our presentation, let's look at a major bottleneck in systems biology: data scarcity. While reconstructing gene regulatory networks requires observing temporal expression patterns over many time steps, real biological experiments are heavily constrained by high costs and technical limitations. Having too few time points directly undermines the accuracy of our network inference algorithms-->
---
layout: default
title:  Why do conventional data augmentation methods fail on sparse transcriptomic data?
eyebrow: LIMITATIONS OF EXISTING METHODS
---
<LimitationsExistingMethods />
<!--Now, you might ask: why not just use standard data augmentation like GANs? Well, GANs are notoriously hard to train on small datasets and frequently suffer from mode collapse. Other synthetic generators rely on overly rigid assumptions. What we desperately need is a simple, stable generative framework that can learn effectively even from a handful of temporal observations.-->
---
layout: default
title:  Can an Autoencoder framework synthesize realistic time-series expression data to restore GRN inference accuracy?
eyebrow: RESEARCH GOALS & HYPOTHESIS
---
<ResearchGoals />
<!--To address this gap, this study asks a fundamental question: Can an Autoencoder learn from a short time series and synthesize remaining time steps reliably? We hypothesize that by encoding adjacent time-step pairs, the model can iteratively generate future time steps, effectively supplementing the missing data and boosting downstream network inference algorithms like MIDNI.-->
---
layout: default
title:  How is the end-to-end Synthetic-MIDNI framework structured?
eyebrow: ARCHITECHTURAL OVERVIEW
---
<SyntheticFramework />
<!--Here is the complete workflow of the Synthetic-MIDNI pipeline. First, raw discretized time-series data is reformatted into concatenated pairwise vectors. Next, we train a custom Autoencoder on these state transitions. The trained model then autoregressively generates the remaining time steps. Finally, both original and synthetic data are fed into the MIDNI algorithm for network reconstruction.-->