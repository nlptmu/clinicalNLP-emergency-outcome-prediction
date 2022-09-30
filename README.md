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
&emsp; For this reason, we used a category-based keyword extraction approach, which calculates the term weighting according to the association between the term and the category. In this way, highly weighted terms indicate a strong association with Emergency department (ED) critical outcomes. This association is determined by calculating `log-likelihood ratio (LLR)` values for every word in the text. 

&nbsp;
&emsp; Next, we employed [Gensim](https://radimrehurek.com/gensim/models/word2vec.html) to train word embeddings for text representation. The clinical narratives are jointly represented by the keyword embeddings. More specifically, the clinical narrative text *__T<sub>k</sub>__* is represented as a weighted average of the keyword vectors, and the weight *__λ<sub>i</sub>__* for a keyword *__K<sub>i</sub>__* is determined by its LLR value. In the case of a clinical narrative without any keyword, we calculated the mean of all word vectors in this clinical narrative and computed cosine similarity over all the keyword vectors to find the closest *__k__* to represent this clinical narrative.  

&nbsp;

![image](https://user-images.githubusercontent.com/74447637/193370371-04886816-2c05-485b-9580-98488af50876.png)

Fig. 1. CNTR calculates the weighted average of nearest keyword vectors when a clinical narrative contains no keywords.


&nbsp;

### **The contribution and insight of CNTR**
* * *

It is an interesting strategy that even if keywords in a clinical narrative are unseen, we can locate the nearest *__k__* words through k-NN and utilize their word embeddings to construct CNTR. In essence, each clinical narrative is projected onto a point in the latent feature space as a distributed representation which can then be evaluated using any classifier. This distributed model of clinical narratives can incorporate a broader amount of context information that covers the entire narrative in the representation. Furthermore, the semantic relations of various surface words can also be captured from the vector space projection of these distributed representations. Such characteristics cannot be easily accomplished in a traditional bag-of-word-based approach, which consumes a significant amount of storage for a sizable n-gram dictionary.

&nbsp;
&emsp; The aim of our method is to support the ED physicians to allow faster identification of high-risk cases, so that they can attend to them promptly. Our proposed method can generate keywords according to the clinical text, so that the model can list the reason or characteristics behind why the patient is predicted to be a high-risk patient, therefore providing interpretability to the physnce of the model.

&nbsp;

### **Source**
* * *
* You can find this tutorial on how to use CNTR for a quick start [here](https://github.com/nlptmu/clinicalNLP-emergency-outcome-prediction/blob/dd5ca8f8c86128a6fbf8536bcf4ea9437688fa82/code/Clinical%20Narratives%20Text%20Representation%20(CNTR).ipynb). All related code is putted at folder named "code".
* You can also find a dictionary of common clinical terms compiled by emergency physicians which is mention in our paper [here](https://github.com/nlptmu/clinicalNLP-emergency-outcome-prediction/blob/9aa6efd244ba963110791388616f0fab57899507/source/Dictionary.xlsx).


&nbsp;

### **References**
* * *

When using our text representation approach for your application, please cite the following paper:
1. Chen, M. C., Huang, T. Y., Chen, T. Y., Panchanit Boonyarat & Chang, Y. C. (Year). Clinical Narrative-aware Deep Neural Network for Emergency Department Critical Outcome Prediction. Journal.
