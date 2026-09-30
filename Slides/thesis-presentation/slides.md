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
<!--
So, what are the common approaches for GRN inference?
There are several major categories of approaches, and each one has its own strengths and limitations.  
**First, correlation-based methods.**  
These methods measure the statistical correlation between pairs of genes. Common examples include **Pearson correlation** and **Spearman rank correlation**.  
Their main advantage is that they are **simple, computationally efficient, and relatively easy to interpret**.  
However, their main limitation is that they primarily capture **pairwise statistical associations**, and therefore may not capture more complex or nonlinear dependencies between genes.  
**Second, information-theoretic methods.**  
Methods such as **ARACNE** and **MIBNI** use information-theoretic measures, particularly **mutual information**, to capture statistical dependencies between genes.  
The main advantage is that mutual information can capture **nonlinear statistical dependencies**, beyond what simple correlation can capture.  
However, these methods can be sensitive to **how the dependency is estimated and how thresholds or other parameters are selected**. In addition, many MI-based approaches have computational challenges as the network size increases.  
**Third, regression and machine learning-based methods.**  
Examples include **GENIE3** and **TIGRESS**.  
These approaches formulate GRN inference as a prediction or feature-selection problem and can model **multivariate relationships** and potentially more complex dependencies.  
However, they can require **model selection and parameter tuning**, and their computational cost can become significant for large networks.  
**Finally, dynamic or time-series models.**  
Examples include **Dynamic Bayesian Networks**, or DBNs, and **ODE-based models**.  
These methods explicitly model **temporal dependencies and gene expression dynamics**, making them particularly relevant to time-series data.  
However, they often require **sufficient time points** and may rely on relatively strong assumptions about the underlying biological dynamics. They can also become   computationally challenging as the network size increases.  
So, overall, different approaches make different trade-offs between **simplicity, the type of dependency they can capture, computational cost, and the amount of temporal information they require**.  
-->
---
layout: default
title: What Have We Done to Improve?
eyebrow: RESEARCH GAPS
---

<ResearchGaps />
<!--
So, what have we done to improve?  
**First**, many existing inference methods represent gene regulation using binary states, which may oversimplify the expression dynamics observed in time-series data.  
**To address this**, we developed a mixed binary-ternary discretization strategy that preserves more regulatory state information.  
**Second**, the availability of large expression datasets is not always matched by representations that allow machine-learning models to effectively exploit the available information.  
**To address this gap**, we developed a scale-invariant task transformation framework that transforms expression profiles into features suitable for GRN inference.  
**Finally**, time-series gene expression datasets often contain only a limited number of observations, making it difficult to learn reliable regulatory relationships.  
**To address this limitation**, we developed a data-generation approach that synthesizes additional time-series expression data to improve inference performance.  
-->
---
layout: default
title: How is gene expression commonly represented for GRN inference?
eyebrow: EXISTING APPROACHES
---

<ExistingApproaches />
<!--
### How is gene expression commonly represented for GRN inference?
According to the **type of data processing**, existing methods can be divided into two groups.  
**Real-value-based methods:**  
In this group, there are some well-known methods such as **GENIE3, MRNET, TIGRESS, and NARROMI**. These approaches directly use continuous values, so they do not need any additional data representation method. Therefore, there is **no information loss** due to data representation. However, these models require more inference time and are sensitive to data noise.  
**Boolean models:**  
To speed up the inference process and handle noise sensitivity, **Boolean models** are widely used, where real-valued data are represented by **0 and 1**. **0** means an off or inhibition state, while **1** denotes an on or activation state. Some well-known methods include **MIBNI and GABNI**. These models require less inference time and are less sensitive to data noise. However, the main drawback is **information loss and dynamic variation due to the simplicity of the data representation**.  
-->

---
layout: default
title: What Do We Want to Improve?
eyebrow: MOTIVATION
---

<Motivations />
<!--
**What do we want to improve?**  
*-First, we want to reduce the computational cost while being less sensitive to noise in gene expression measurements.*     
*-At the same time, we aim to preserve more expression-level information than conventional Boolean representations.*    
*-Finally, we want to improve both the accuracy of the inferred network structure and its dynamic behavior.*  
-->
---
layout: default
title: What is the Pipeline?
eyebrow: PIPELINE
---

<Pipeline01 />
<!--
On the screen, you can see the pipeline of the proposed framework.
It can be divided into **four main stages**.  
**First, we prepare the gene expression profiles.**  
**Second, the discretization stage.**  
We transform continuous expression values into multiple discrete states — in our case, **two or three levels**, depending on the distribution of each gene.  
**Third, we infer regulatory relationships** from the discretized time-series profiles using information-based feature selection. At this stage, **two routines are conducted**.  
**Finally, we evaluate the inferred network** from both **structural and dynamic perspectives**.  
Key contributions are stages 2 and 3.
-->

---
layout: default
title: How Does the Discretization Network Model Represent Gene Dynamics?
eyebrow: DISCRETIZATION NETWORK MODEL
---

<DiscretizationNetworkModel />
<!--
Before going into our proposed model, let us first take a quick look at some basic concepts of a **discrete-state network model**.  
First, a discretized network can be represented as a **directed graph**.  
We have a set **V**, which contains all the nodes in the network, and a set **A**, which represents the interactions between these nodes.  
For each node *g*, its state at time *t* is represented by one of **l discrete values**, ranging from **0 to l minus 1**.  
Now, suppose that a target node *g* is regulated by *k* other genes, from *u₁* to *uₖ*.  
Then, the state of node *g* at time *t plus 1* is updated according to a **discrete function**, as shown on the screen.  
In other words, the future state of a target gene is determined by the current states of its regulatory genes.  
-->
---
layout: default
title: How Do We Evaluate an Inferred Network?
eyebrow: PERFORMANCE EVALUATION
---

<NetworkInference />
<!--
We evaluate the inferred networks from two perspectives: **dynamics and structure**.  
For the **dynamics**, first, we define the gene-wise dynamics consistency, \(C(v,v')\), as the similarity between the discretized trajectories of the observed gene expression, \(v(t)\), and the estimated gene expression, \(v'(t)\).   
Then, the **dynamics accuracy** is defined as the average gene-wise dynamics consistency across all genes.  
For the **structural evaluation**, we use three metrics: **Precision, Recall, and Structural Accuracy**.  
**Precision** measures the proportion of inferred regulatory interactions that are actually correct.   
**Recall** measures the proportion of true regulatory interactions that are successfully recovered.  
Finally, **Structural Accuracy** measures the overall agreement between the inferred network and the ground-truth network structure.
-->
---
layout: default
title: What is the experimental framwork?
eyebrow: METHODOLOGY
---

<Methodology />
<!--
Let me now give you an overview of the proposed framework.  
We start with a **two-dimensional microarray of real-valued gene expression data**, which is observed from an underlying regulatory network. Importantly, **the original network itself is unseen during the inference process**.  
First, this input expression matrix is converted into a **discretized expression dataset** using the K-means discretization algorithm.  
Then, the **K value is determined based on a validity index for each gene**. In this study, K can be either **2 or 3**, depending on the expression distribution of each gene.  
Next, the discretized data are fed into the **MIFS and SWAP subroutines** to identify the regulatory genes for each target gene.  
Based on the inferred regulatory relationships, we reconstruct the **prediction network**. At the same time, the prediction network provides the corresponding **inferred discretized expression values**.  
Finally, at the evaluation stage, we compare the **inferred network with the ground-truth network** to evaluate the structural accuracy. For the dynamics accuracy, we compare the **observed and inferred discretized expression matrices**.
-->
---
layout: default
title: How Do We Determine the Optimal Discretization Level?
eyebrow: DISCRETIZATION
---

<Discretization />
<!--As mentioned above, in our study, the discretization level of each gene can be either two or three.  
To determine the optimal level, we apply a validity index, which is defined as the ratio of the Intra value to the Inter value.   
The Intra value is the average squared distance between data points and their corresponding centroids.   
The Inter value is the minimum squared distance between two different centroids. Therefore, the optimal discretization level is selected by minimizing the validity index.
-->
---
layout: default
title: How Are Potential Regulators Selected and Refined?
eyebrow: FEATURE SELECTION
---

<FeatureSelectionStage />
<!--
* For each target gene g₀, MIFS selects a set of k potential regulator genes. The value of k is a user-defined parameter. In this study, the maximum value of k is 8.
* MIFS can be described in 3 steps:  
  * Step 1: Select a gene that maximizes the mutual information with g₀.   
  * Next, select the gene that maximizes the mutual information with g₀ while considering its dependency on the already selected candidates.   
  * Repeat Step 2 until the desired number of k candidates has been selected.  

The main drawback of the MIFS subroutine is that it does not compute the exact multivariate mutual information and may fail to find the optimal set of regulatory variables.  
To overcome this problem, we propose a simple iterative SWAP subroutine to improve the dynamics accuracy by swapping the same number of variables between the selected and unselected sets.  
The swapping process is repeated until the gene-wise dynamics consistency reaches 1.0, meaning that there is no further improvement, or until the number of potential candidates in the selected set equals k.  
-->
---
layout: default
title: Which Datasets Are Used for Evaluation?
eyebrow: DATASETS
---

<Datasets01 />
<!--
*We tested the proposed method using two types of datasets: Artificial Discretized and GNW datasets.*  
*The Artificial Discretized dataset consists of 20 network groups, with network sizes ranging from 10 to 200. Each group contains 20 randomly generated networks, resulting in a total of 400 networks.*   
*The GNW dataset consists of 4 network groups with network sizes of 50, 100, 200, and 300. Each group contains 20 networks, a total of 80 networks were tested.*
-->
---
layout: default
title: How Does Three-Level Proportion Vary?
eyebrow: THREE-LEVEL PROPORTION
---

<Proportion />
<!--
We first examined the proportion of three-level discretized genes in the networks.   
As shown in the figure, the proportions of the binarized and three-level discretized genes are considerably similar to each other.  
This indicates that three-level discretization is observed as frequently as two-level discretization in our method.  
-->
---
layout: default
title: Does the Proposed Method Perform Well across All Metrics?
eyebrow: RESULTS - ARTIFICIAL DATASET
---

<ArtificialResults />
<!--
* This figure shows the performance of our method on the Artificial Discretized dataset using four evaluation metrics.
* The X-axis represents the network size, ranging from 10 to 200, while the Y-axis shows the average value of each performance metric.
* Looking at the figure, we can see that:  
  * Dynamics accuracy consistently reaches a perfect value of 1.0 across all network sizes.   
  * Structural accuracy remains above 0.9.  
  * Precision and recall decrease as the network size increases, but both remain above 0.5 at a network size of 200.  
* In short, our method shows reliable performance on this dataset.  
-->
---
layout: default
title: How Does Network Complexity Affect Inference Performance?
eyebrow: RESULTS - ARTIFICIAL DATASET
---

<IncomingLinksResults />
<!--
* We also show the performance on this dataset by grouping the number of regulatory genes for each target gene in the gold-standard network, as shown on this slide.
* As the number of incoming links increases, the performance metrics decrease because a larger number of incoming links indicates a more difficult inference problem.
* As shown in this figure:
  * Dynamics accuracy remains almost stable, even in the most difficult case, when the number of incoming links is 8.
  * Precision and recall remain above 0.4.
-->
---
layout: default
title: How Well Does the Inferred Network Recover the True Structure?
eyebrow: RESULTS - ECOLI DATASET
---

<StructuralAccuracy />
<!--
*This slide shows the structural accuracy of our method and four comparison methods across four network sizes: 50, 100, 200, and 300.*
*Overall, MIDNI shows better performance than the other methods.*
*Furthermore, across the four network sizes, when the number of incoming links is 1 or 2, the performance of all methods is relatively similar. However, as the number of incoming links increases, our method shows better performance than the others.*
*This indicates the effectiveness of our method for large-scale and difficult-to-solve GRN inference problems.*
-->
---
layout: default
title: How Well Does the Model Explain the Underlying Mechanism?
eyebrow: RESULTS - ECOLI DATASET
---

<DynamicsAccuracy />
<!--
* Here, we show the dynamics accuracy of all methods across four network sizes: 50, 100, 200, and 300.  
* Similar to the structural accuracy, the dynamics accuracy of the proposed method is higher than that of the other methods, especially for larger networks of size 200 and 300.  
* Taken together, MIDNI outperforms the comparison methods in terms of both structural and dynamics accuracy.  
-->
---
layout: default
title: How Does Computational Efficiency Vary Across Methods?
eyebrow: RUNNING TIME
---

<RunningTime />
<!---
We also conducted a comparison with running time among the methods. The result is shown on this figure.  
Look at the chart, our method is comparable to others except dbn method.  
Briefly, MIDNI is a promising tool for predicting both the structure and the dynamics of a gene regulatory network, especially for large-scale and dense input networks.  
-->
---
layout: default
title: What Have We Achieved, and What Remains to Be Improved?
eyebrow: CONCLUSION
---

<Conclusion />
<!--
What we achieved?
- Infer regulatory networks using a multiple level representation beyond Boolean states
- Achieve higher structural and dynamics accuracy than the comparison methods
- Maintain reliable inference performance as network size and connectivity increase
What are limitations?
- Repy on correlation coefficients to determine the type and direction of regulatory interactions
- MIFS and SWAP are essentially greedy algorithms and may not guarantee a globally optimal feature selection.
-->
---
layout: default
title: Why do existing machine learning frameworks still fail to generalize?
eyebrow: RESEARCH GAP 02
---
<RepresentationMotivations />
<!-- CHAPTER 3 -->
<!--
*“In the first issue, I focused on the inference method. By introducing multiple-level discretization, we can preserve more information from gene expression dynamics than a purely Boolean representation.*  
*However, when moving toward machine learning, another question arises: how should a regulatory relationship be represented so that a learning model can actually learn from it? This question motivates the second issue addressed in this chapter.*  
*First, let us look at why existing machine learning frameworks still fail to generalize.*   
*First, temporal expression dynamics and local regulatory structures are encoded separately or indirectly.*   
*Second, models depend heavily on fixed time delays, restricted candidate regulator sets, or specific kernel configurations.*  
*Finally, sparse networks lead to class imbalance, meaning that as the network scale increases, the ratio of positive regulatory interactions to non-interactions becomes increasingly skewed.* 
 -->
---
layout: default
title: How did we build a learning framework for GRN inference?
eyebrow: PROPOSED FRAMEWORK
---
<LearningFramework />
<!--
“This slide shows an overview of the proposed GRN inference framework.  
We start with labeled gene regulatory networks with known regulatory interactions. These networks are transformed into a supervised learning dataset using our representation scheme, which converts time-series expression profiles into feature-label pairs.  
The resulting features are used to train different machine learning models, which are stored in a classifier pool.  
For inference, the test expression data are represented in the same way and processed by a selected model to predict pairwise regulatory interactions. These predictions are then aggregated to reconstruct the inferred GRN.  
Importantly, our representation is independent of network size, allowing models trained on one network size to generalize to networks of different sizes.”  
-->
---
layout: default
title: How is gene profile reformulated into a binary classification task?
eyebrow: DATA REPRESENTATION
---
<DataRepresentation />
<!--
"Let's look at how we represent the data to turn GRN inference into a task machine learning can solve."  
"First, each gene Gi is represented as a time-series vector across T observed time points — this is our raw input."  
"Next, to capture the relationship *between* two genes, we concatenate the regulator's and target's expression vectors into a single 2T-dimensional feature vector."  
"Then, each gene pair is labeled 1 if a directed interaction exists in the gold standard, and 0 otherwise."  
"Finally, applying this across all gene pairs gives us a fully labeled dataset, where each sample is one candidate regulatory interaction."  
"In short, this representation turns GRN inference into a supervised binary classification problem — making it scalable and model-agnostic."
-->
---
layout: default
title: What unique advantages does the unified representation offer?
eyebrow: METHODOLOGICAL HIGTLIGHTS
---
<MethodAdvantages />
<!--What makes this representation so effective? 
First, it’s completely assumption-free—the model learns temporal dependencies implicitly without manual time-lag tuning.  
Second, it encodes structure and time dynamics together.   
And most importantly, because feature length depends only on time steps $T$ rather than gene count, it creates a scale-invariant feature space.
-->
---
layout: default
title: How were the datasets and evaluation metrics configured?
eyebrow: EXPERIMENTAL SETUP
---
<ExperimentalSetup />
<!--
*Moving on to our experimental setup, we evaluated the framework on two benchmarks: synthetic scale-free Barabási–Albert networks and realistic E. coli networks from GeneNetWeaver.*  
*For the topological datasets, we tested three network sizes: 10, 50, and 100. The training set contains 20,000, 2,000, and 2,000 ground-truth networks for each size, respectively. The validation and test sets contain 2,000, 400, and 400 networks, respectively.*  
*For the E. coli dataset, we also tested three network sizes: 10, 50, and 100. The training set contains 200, 20, and 20 network structures, respectively, with 100 time-series samples generated for each structure. The validation sets contain 20, 4, and 4 structures, while the test sets contain 10, 4, and 4 structures, respectively.*   
*Because true regulatory interactions are extremely sparse in biological networks, we use AUPR as our primary evaluation metric rather than AUROC. AUPR ranges from 0 to 1, with a value closer to 1 indicating better performance.*  
-->
---
layout: default
title: How did models perform on scale-free topological networks?
eyebrow: RESULTS - TOPOLOGICAL NETWORKS
---
<AUPRToys />
<!--
-On the synthetic topological datasets, every single machine learning model outperformed the random baseline.   
-Random Forest delivered the highest overall accuracy across all network sizes.   
-Interestingly, Gaussian Naive Bayes was the only model whose performance actually improved as network size grew, thanks to its strong probabilistic inductive bias  
-->
---
layout: default
title: Does the framework outperform traditional GRN inference methods on biological data?
eyebrow: RESULTS - BIOLOGICAL NETWORKS
---
<AUPREcoli />
<!--
When tested on biological E. coli networks, the performance gap expanded even further.   
The supervised learning models achieved dramatically higher AUPR scores than traditional algorithms like Jump3 or Inferelator.   
GNB consistently emerged as the most reliable model across all network dimensions.  
-->
---
layout: default
title: Can models trained on small networks effectively infer large-scale GRNs?
eyebrow: RESULTS - KEY FINDINGS
---
<KeyFindings />
<!--
“Now, let’s highlight our key discovery: **scale invariance**.  
We trained three GNB models using training sets of different sizes: 5,000, 10,000, and 20,000 network structures. After training, each model was evaluated on test networks with three different sizes: 10, 50, and 100 genes. We then compared these results with models trained directly on networks of the corresponding sizes.   
The results are shown in the chart on the left.   
We can highlight that a GNB model trained exclusively on small 10-gene networks achieved an AUPR of 0.373 on 50-gene networks and 0.333 on 100-gene networks. These results are comparable to, and in some cases better than, models trained directly on larger networks. This demonstrates that interaction-level knowledge can transfer effectively across different network scales.  
The chart on the right shows the training time of the models. The results demonstrate that training on smaller networks can significantly reduce training time and computational resources, while maintaining comparable inference performance to models trained on larger networks.  
-->
---
layout: default
title: Can the Model Maintain Its Performance with Fewer Time Steps?
eyebrow: RESULTS - KEY FINDINGS
---
<TimeStepVariation />
<!--
“Now, in real-world experiments, gene expression data often contain only a limited number of time points. Therefore, we conducted an experiment to investigate whether the model can maintain its performance with fewer time points.  
We trained the models using three datasets with different numbers of time points: 10, 20, and 50, across the three network sizes. The results are shown in the chart on this slide.  
Except for the size-10 networks, where fewer time points actually achieved better performance, the results are generally consistent across the different time-point settings. One possible explanation is that, for smaller networks, fewer time points may reduce noise and help the model make more accurate predictions.    
More importantly, even with only 10 time points, the model still achieves relatively high inference performance in the other cases. This suggests that the proposed framework has promising potential for practical applications with limited time-series observations.”
-->
---
layout: default
title: What are the computational cost advantages of small-network training?
eyebrow: COMPUTATIONAL PERFORMANCE
---
<ComputationalComparison />
<!--
From a computational standpoint, training on small networks saves 15% to 25% in training time compared to large-scale training.  
Furthermore, while traditional methods have to re-compute everything from scratch for every new dataset,   
our pre-trained classifiers run online inference in a fraction of a second.
-->
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
