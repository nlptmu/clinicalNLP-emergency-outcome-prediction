# clinicalNLP-emergency-outcome-prediction
## Clinical Narratives Text Representation (CNTR)

### Table of contents
- The introduction of CNTR
- The contribution and insight of CNTR
- Source
- References


&nbsp;
### **The introduction of CNTR**
* * *


Since the performance of text classification benefits from efficient text representation, we present the `Clinical Narratives Text Representation (CNTR)` based on embeddings, which is used in this study to develop correlation between critical outcomes and clinical narratives (i.e., medical history, chief complaints and present illness). The inspiration behind CNTR comes from  the observation of how critical care physicians are able to identify an ICU case by means of important lexicon or semantic contents in order to rapidly narrow down the scope of possible candidates. For instance, when an expression contains keywords such as “ICH (intracerebral hemorrhage)”, “SAH (subarachnoid hemorrhage)” and “aortic dissection”, we can conclude that the expression very likely contains crucial information. This assumption can be used to explain how critical care physicians are able to browse through the clinical narrative quickly to capture key information of the ICU case. 

&nbsp;
&emsp; For this reason, we used a category-based keyword extraction approach, which calculates the term weighting according to the association between the term and the category. In this way, highly weighted terms indicate a strong association with Emergency department (ED) critical outcomes. This association is determined by calculating `log-likelihood ratio (LLR)` values for every word in the text. We define the patient who has a high-risk of admission to an ICU or IHCA as a positive case, and a patient who has low risk as a negative case. As presented in Equation (1), *HR* is defined as a patient with a high-risk of admission to an ICU or at high-risk of IHCA, otherwise it is not a high-risk case *(¬ HR)*. We let *k* denote the number of high-risk cases’ clinical narratives containing a word *w*, and *l* denote the number of clinical narratives including *w* but which are not high-risk cases. In addition, *m* denotes the number of clinical narratives of high-risk cases without *w*, and *n* denotes the number of clinical narratives of non-high-risk cases without *w*. The word with a higher LLR value has a stronger relation to a certain ED disposition. A maximum likelihood estimation is performed to obtain probabilities *p(w)*, *p(w|HR*), and *p(w|¬HR)*.  

&nbsp;

$$LLR(w,HR)=2log⁡\left[\frac{p(w|HR)^k (1-p(w│HR))^m p(w|¬ HR)^l (1-p(w│¬HR))^n)}{p(w)^(k+l) (1-p(w))^(m+n)}\right]![image](https://user-images.githubusercontent.com/74447637/193268962-f8e22837-5429-40a6-81ce-50ce6cdf4517.png) &emsp; (1)$$  
  
  
&nbsp;  

&nbsp;
&emsp; Next, we employed `Gensim` to train word embeddings for text representation. The clinical narratives are jointly represented by the keyword embeddings. More specifically, the clinical narrative text Tk is represented as a weighted average of the keyword vectors, and the weight λi for a keyword Ki is determined by its LLR value. In the case of a clinical narrative without any keyword, we calculated the mean of all word vectors in this clinical narrative and computed cosine similarity over all the keyword vectors to find the closest k to represent this clinical narrative.

&nbsp;

### **The contribution and insight of CNTR**
* * *

It is an interesting strategy that even if keywords in a clinical narrative are unseen, we can locate the nearest k words through k-NN and utilize their word embeddings to construct CNTR. In essence, each clinical narrative is projected onto a point in the latent feature space as a distributed representation which can then be evaluated using any classifier. This distributed model of clinical narratives can incorporate a broader amount of context information that covers the entire narrative in the representation. Furthermore, the semantic relations of various surface words can also be captured from the vector space projection of these distributed representations. Such characteristics cannot be easily accomplished in a traditional bag-of-word-based approach, which consumes a significant amount of storage for a sizable n-gram dictionary.

&nbsp;
&emsp; The aim of our method is to support the ED physicians to allow faster identification of high-risk cases, so that they can attend to them promptly. Our proposed method can generate keywords according to the clinical text, so that the model can list the reason or characteristics behind why the patient is predicted to be a high-risk patient, therefore providing interpretability to the physnce of the model.

&nbsp;

### **Source**
* * *

&nbsp;

### **References**
* * *

When using our text representation approach for your application, please cite the following paper:
1. Chen, M. C., Huang, T. Y., Chen, T. Y., Panchanit Boonyarat & Chang, Y. C. (Year). Clinical Narrative-aware Deep Neural Network for Emergency Department Critical Outcome Prediction. Journal.
