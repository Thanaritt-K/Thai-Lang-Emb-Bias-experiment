# Examination of Bias in popular Thai language embeddings
## Information  
Thanaritt Kunajak  
Natural Language Processing  
Master’s in Theoretical and Applied Linguistics (8037)  
Universitat Pompeu Fabra  
Exercise 3

## 1 Introduction

In the context of AI systems, the term bias can have manifold meanings and may not be explicitly defined. Notions of bias on the societal level, already nuanced, collide with bias in the context of statistics and data science.(Puttick et al., 2025) While clear-cut definition or classification of bias is difficult to make, highlighting the complexity and often contentious nature of the concept, bias was historically understood in neutral terms—as a mere deviation from a standard —such deviations frequently involve value-laden, normative judgments that reflect societal structures of privilege and oppression, influencing individual reasoning, actions, and well-being. (Danks & London, 2017) In this experiment, I would like to focus only on Diversity Bias, specifically the discrimination based on Gender. 

A large body of work has been developed to detect (and partially mitigate) these biases. These efforts have been summarized in various literature reviews (Sun et al. 2019; Meade et al. 2022; Delobelle et al. 2022). An early detection and mitigation method was developed by Bolukbasi et al. (2016) and relied on attempting to delete gender information from word embeddings by contracting the vector subspace corresponding to gender. Another well-known method for bias detection in static word embeddings was proposed by Caliskanet al. (2017). Drawing from the implicit association test (IAT) (Greenwald et al. 1998) used in psychology to detect implicit bias in human subjects, the method was adapted for and applied to static word embeddings. 

Despite this extensive body of work, research addressing the detection of bias in word embeddings and language models is significantly skewed towards the English language. This poses a real problem because research indicates that (encoded) stereotypes are often language-dependent and impacted by cultural context, as evidenced both in psychological research (e.g., Fiske 2017) and in the context of word embeddings (e.g., Kurpicz-Briki and Leoni 2021). And from the body of research available regarding Thai NLP, there has been none on the detection and mitigation of Bias.

## 2 Material and methods

### 2.1 Data Sources

In this experiment I’ll examine Typhoon-S (Pipatanakul & Taveekitworachai, 2026) (https://huggingface.co/typhoon-ai/typhoon-s-thaillm-8b-instruct-research-preview), an upcoming "Sovereign", instruction-tuned Thai large language model, which is based on Qwen3. (Yang et al., 2025). The reason is due to the Typhon project’s popularity and adoption rate in Thailand, boasting the most downloads and usage by the community. (Pipatanakul et al., 2023)

### 2.2 Preprocessing steps

In this experiment I’ll use Sentence Encoder Association Test (SEAT) as proposed by May et al (2019), which is an extension of Word Embedding Association Test (WEAT) by Caliskanet al. (2017). SEAT is a statistical test that detects bias in sentence embeddings using cosine similarity and averaging methods, paired with hypothesis testing.

To extend a word-level test to sentence contexts, each word will be slotted into each of several semantically bleached sentence templates. And so, in addition to coming up with Thai terms equivalent to the ones used in previous studies, I’ll have to also come up with these sentence templates.

### 2.3 Evaluation Metrics 

Let X and Y be equal-size sets of target concept embeddings and let A and B be sets of attribute embeddings. The test statistic is a difference between sums over the respective target concepts, where each addend is the difference between mean cosine similarities of the respective attributes,

A permutation test on s(X, Y, A, B) is used to compute the significance of the association between (A, B) and (X, Y ), where the probability is computed over the space of partitions (Xi, Yi) of X ∪ Y such that Xi and Yi are of equal size, and a normalized difference of means of s(w, A, B) is used to measure the magnitude of the association (the effect size; Caliskan et al., 2017),

Controlling for significance, a larger effect size reflects a more severe bias.

## 3 Results

The result doesn’t show a high enough significant P-value.This result also echoes points made by May et al (2019), regarding the result showing that sentence encoders exhibit less bias than previous word-embedding models. However, there are multiple points to be made regarding this lack of bias. First, it is unclear whether each set of words or sentences in these tests represents a coherent concept/attribute (like Gender or Career-related) to the sentence encoders.  Second, cosine similarity might be an inadequate measure of text similarity for sentence encoders, since cosine distance is a linear space where all dimensions are weighted equally. Third, Like WEAT, SEAT only has positive predictive ability: It can detect presence of bias, but not its absence. Considering that these representations are trained without explicit bias control mechanisms on naturally occurring text, it should be argued against interpreting a lack of evidence of bias as a lack of bias.

## 4 Code

The code to the experiment is available online at: [Thai-Lang-Emb-Bias-experiment](https://github.com/Thanaritt-K/Thai-Lang-Emb-Bias-experiment)
