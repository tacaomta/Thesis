---
title: "GRN Inference — PhD Thesis"
titleTemplate: "%s"
layout: thesis-cover
---

<template #network>
  <ThesisNetwork />
</template>

<!--
-Good morning, committee members, and good morning, everyone.

-My name is Kao, and I am a Ph.D. student from the Complex Systems Computing Lab.

-Today, I am going to present my Ph.D. thesis, entitled **“Inferring Gene Regulatory Networks from Time-Series Gene Expression Profiles.”**

-This work was conducted under the supervision of Professor Yung Keun Kwon.
-->

---
layout: default
title: "From Better Inference to Better Data"
eyebrow: "THESIS OVERVIEW"
---

<ThesisOverview />

<!--
Here is an overview of my thesis.

The overall research flow is **from better inference to better data**.

First, I will introduce the **research problem**, answering two fundamental questions: **What is a Gene Regulatory Network, and why do we need time-series gene expression data?**

This part defines the research challenges, identifies the existing gaps, and presents the objectives of this thesis.

Second, I will present a **Mutual Information-based GRN inference method**.
In this work, I develop a GRN inference method based on **multiple-level discretization and mutual information**.

Next, I will introduce a **Scale-Invariant Task Transformation Framework for GRN inference**.
This work addresses the question: **“Can informative representations be learned automatically from time-series gene expression data?”**

Finally, I address the question: **“How can we improve GRN inference performance when only limited time-series gene expression data are available?”**

To address this challenge, we use an **autoencoder to generate synthetic gene expression profiles**, and then validate the generated data through GRN inference methods.

-->

---
layout: default
title: What is a Gene Regulatory Network?
eyebrow: GENE REGULATORY NETWORK
---

<GRNs />
<!---
-Now, let me clarify what a **Gene Regulatory Network**, or GRN, is.  
-A GRN describes the regulatory relationships among genes and how these relationships influence gene expression.  
-On this slide, you can see an example of a GRN.  
-Each **node represents a gene**. A gene can act as a **regulator**, influencing other genes, or as a **target gene**, whose expression is regulated.   
-The **directed edge represents a regulatory influence** from one gene to another.  
-There are two main types of regulatory influence. An **enhancing or activating interaction** increases the expression of the target gene, while an **inhibitory interaction** decreases its expression.  
-So, briefly, a **GRN is a set of genes connected by directed regulatory relationships**.
-->

---
layout: default
title: What are we actually Trying to Infer?
eyebrow: RESEARCH PROBLEM
---

<InferenceProblem />
<!--
So, what are we actually trying to infer?  
To answer this question, let us first look at what happens in the biological world.  
Inside a cell, regulatory mechanisms and regulatory processes are continuously taking place. However, we cannot directly observe these processes.  
Instead, we assume that there is a **hidden regulatory network** that describes **who regulates whom**.  
Through these regulatory interactions, the activity of regulatory genes influences the expression of their target genes. As a result, gene expression levels change over time.  
Importantly, **these changes in gene expression are something that we can observe and measure**.    
Therefore, in an experiment, what we actually obtain are **gene expression profiles** — measurements of gene expression collected across multiple time points.  
However, what we really want to know is not just the expression levels themselves. We want to uncover the **underlying regulatory relationships among genes** that generate these observed expression dynamics.   
Therefore, by applying computational techniques and GRN inference methods, we try to reconstruct the **hidden regulatory network from the observed time-series gene expression profiles**.  
In other words, **we observe gene expression, but we want to infer the regulatory relationships behind it**.  
-->

---
layout: default
title: Why do Regulatory Genes Matter?
eyebrow: WHY DOES IT MATTER?
---

<RegulatoryGenes />
<!--
So, why do regulatory genes matter?  
Identifying regulatory genes and their target genes can help us better understand how biological systems are controlled.  
First, it helps us understand **how genes regulate other genes**, and therefore reveals the regulatory relationships within the cell.  
Second, it helps us understand **how cellular processes are coordinated** by connecting gene regulation to downstream biological responses.  
Furthermore, regulatory networks can help us understand **how cells respond to changes in different biological or external conditions**, such as temperature, pressure, or other environmental stimuli.  
More importantly, by identifying regulatory genes and their targets, we can also identify **key control points within the regulatory network**.  
Ultimately, understanding these regulatory mechanisms can provide valuable insights into **disease mechanisms** and may help identify **potential therapeutic targets**.  
Therefore, identifying regulatory relationships is important not only for understanding basic biological processes, but also for understanding how cells respond and adapt to different conditions.  
-->
---
layout: default
title: What Data Do We Observe?
eyebrow: EXPERIMENTAL DATA
---

<ObservedData />
<!--
So, what data do we actually observe?  
In experiments, we measure **gene expression levels over time**. These time-series gene expression data can be represented as a two-dimensional matrix.  
In this matrix, the **columns correspond to genes**, represented by their gene names or gene indices, while the **rows correspond to different time points**.  
Therefore, each cell contains the **expression value of a specific gene at a specific time point**.  
In general, there are two common ways to measure gene expression: **steady-state measurements and time-series measurements**.  
So, why do we use time-series data?  
Unlike steady-state measurements, which capture gene expression at a particular condition or time point, **time-series data capture the temporal dynamics of gene expression**.  
For example, we can observe whether the expression of a gene **increases, decreases, or remains relatively stable over time**.  
Moreover, instead of observing only a single static state, time-series data provide **multiple observations that form a trajectory**, giving us more information about how gene expression changes over time.  
More importantly, these temporal patterns can provide **clues about regulatory dependencies between genes**. For example, changes in one gene may precede or be associated with changes in another gene, providing information that can be useful for reconstructing regulatory relationships.  
Therefore, time-series gene expression data provide not only information about **what the expression level is**, but also about **how it changes over time**.   
-->
---
layout: default
title: Why is Time-series GRN Inference Difficult?
eyebrow: CHALLENGES
---

<TimeSeriesDifficulty />
<!--
So, what are the main challenges in inferring a Gene Regulatory Network?
There are several important challenges.  
**First, high dimensionality.**  
In real-world biological systems, we may need to infer regulatory relationships among **thousands of genes**. As the number of genes increases, the number of possible regulatory relationships grows dramatically.  
**Second, limited observations.** Although we may have thousands of genes, the number of available time points is often relatively small. In other words, we have a **high-dimensional problem with limited observations**.  
**Third, noise and biological variability.**Gene expression measurements can contain experimental noise and biological variation. These factors can make it more difficult to distinguish true regulatory signals from random variations, and therefore can reduce the accuracy of GRN inference.   
**Fourth, complex regulatory dependencies.**Gene regulatory systems can involve **nonlinear relationships, self-regulation, feedback loops, and other complex dependencies**. Capturing these relationships from gene expression data is challenging.  
**Finally, the problem is inherently ambiguous.**Different network structures may produce **similar or even indistinguishable expression patterns** under the observed conditions. Therefore, recovering the underlying regulatory network from expression data is a challenging inference problem.   
Together, these challenges make GRN inference difficult, especially when we have **many genes but only limited and noisy time-series observations**.
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
---
layout: default
title:  How does pairwise temporal vector concatenation preserve transition dynamics?
eyebrow: FEATURE ENGINEERING
---
<FeatureEngineering />
<!--A critical innovation here lies in data representation. Instead of feeding single time steps, we concatenate expression values from two consecutive steps, $t_i$ and $t_{i+1}$. This $2n$-dimensional vector explicitly captures state-transition relationships, giving the neural network the exact temporal signals it needs to predict the next time step.-->
---
layout: default
title:   What is the design and parameter configuration of the generative Autoencoder?
eyebrow: AUTOENCODER ARCHITECTURE
---
<DeepLearningArchitecture />
<!--Let's examine the Autoencoder architecture itself. We chose a lightweight 3-hidden-layer design with a 32-neuron bottleneck layer. Why keep it compact? Because a smaller architecture prevents overfitting on limited biological samples and keeps training stable. It uses ReLU activations in hidden layers and minimizes mean squared error during training.-->
---
layout: default
title:   How does the model perform iterative auto-regressive time-series synthesis?
eyebrow: GENERATIVE MECHANISM
---
<GenerativeMechanism />
<!--So how does the model actually generate new time points? It works iteratively. When you pass $\mathbf{T}(t_i \oplus t_{i+1})$ into the trained model, it outputs the predicted state for $\mathbf{T}(t_{i+1} \oplus t_{i+2})$. We extract the newly predicted time point and loop it back into the model as input for the next step, repeating this until we reach our target series length.-->
---
layout: default
title:   How Was the Experimental Setup Designed?
eyebrow: EXPERIMENTAL SETUP
---
<ExperimentalSetup04 />
<!--To evaluate performance rigorously, we generated 20 scale-free ground truth networks representing 50-gene and 100-gene biological systems. We fixed the total trajectory length at 100 time steps while systematically varying observed steps $K$ from 10 to 90. This allowed us to benchmark inference improvements under varying degrees of data availability. This brings us to our evaluation metrics.-->
---
layout: default
title:  Which Metrics Are Used to Evaluate GRN Inference?
eyebrow: EVALUATION METRICS
---
<EvaluationMetrics />
<!--We evaluated performance using four quantitative metrics. Precision, Recall, and Structural Accuracy measure how accurately edge connections match ground truth networks. Meanwhile, Dynamic Accuracy calculates trajectory preservation using Hamming distance across time steps. Let's now examine the structural performance results on multi-level ternary data.-->
---
layout: default
title:  How well performance gains on ternary datasets?
eyebrow: RESULTS - TERNARY DATASETS
---
<TernaryDatasetsRecovery />
<!--Looking at the results for ternary datasets, solid lines—representing synthetic data augmentation—consistently outshine the dashed baseline lines. Crucially, the improvement is largest at $K=10$ and $K=20$, proving that synthetic data provides the highest value precisely when experimental samples are most scarce. Let's see if these gains hold true for Boolean datasets as well.-->
---
layout: default
title:  How well performance gains on Boolean datasets?
eyebrow: RESULTS - BOOLEAN DATASETS
---
<BooleanDatasetsRecovery />
<!--Moving to Boolean datasets, we observe the exact same positive trend. Synthetic data enhances inference performance without introducing negative artifacts. Interestingly, smaller 50-gene networks saw larger recall boosts, whereas larger 100-gene networks achieved higher precision gains. Having confirmed structural recovery, let's transition to evaluating dynamic fidelity.-->
---
layout: default
title: How Well Is Dynamic Fidelity Preserved?
eyebrow: RESULTS - DYNAMICS FIDELITY
---
<DynamicsFidelity />
<!--Now, addressing dynamic accuracy: you might notice a slight downward trend as time steps increase. This happens because synthetic-driven networks are evaluated over the entire 100-step timeline, while original data is tested over shorter $K$ steps. Nevertheless, dynamic accuracy remains well above 97%, proving that generated time-series retain strong biological state fidelity. Next, let's examine data diversity.-->
---
layout: default
title: How Diverse Are the Synthesized Expression Profiles?
eyebrow: RESULTS - DATA DIVERSITY ANALYSIS
---
<DataDiversity />
<!--A fascinating aspect of this method is data diversity. When executing the autoencoder multiple times, generated expression matrices differ significantly, exhibiting a similarity index around 0.35 to 0.40. Remarkably, downstream network inference remains stable across these diverse profiles. This mirrors real biology, where distinct expression fluctuations stem from the same core regulatory network. Let's move to our conclusion.-->
---
layout: default
title: What are Key Findings and Biological Significance?
eyebrow: SUMMARY AND IMPLICATIONS
---
<SummaryOfCoreFindings />
<!--To summarize our core findings, this study proves that a lightweight autoencoder can effectively synthesize temporal gene expression data to overcome sample scarcity. By augmenting short experimental series, researchers can reconstruct significantly more accurate gene regulatory networks without incurring heavy laboratory expenses. Finally, let's discuss future research horizons.-->
---
layout: default
title: Where Can This Research Go Next?
eyebrow: FUTURE HORIZONS
---
<FutureHorizons />
<!--Looking forward, there are several promising avenues for future research. Integrating Graph Neural Networks could help model structural topologies directly. Transitioning to continuous-valued modeling will eliminate discretization artifacts. Finally, validating this method on clinical transcriptomic datasets—such as rare disease models—will unlock immense real-world value. Thank you for your time, and I am happy to take any questions!-->
