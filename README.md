# News-Polarity-Detection

News Polarity Detection   
Problem Statement - 
We address the problem of determining entity-oriented polarity in business news. This can be viewed as classifying the polarity of the sentiment expressed toward a given mention of a company in a news article. We focus on determining the polarity of a mention of a given company in news media. Polarity classification is important, since if a company appears in negative contexts frequently, it may affect its reputation, impact its stock price, etc.

Description - 
Polarity prediction is similar to sentiment analysis both requiring the system to classify a span of text as positive or negative. A key NE (Named Entity) in business news type is company or organisation, which can be mentioned in a positive or negative context. For example, launching a new product or signing a new contract is viewed as a positive event; involvement in a product recall, bankruptcy or fraud is considered negative. However, there are crucial differences. Business news articles typically do not aim to express emotion or subjectivity—positive and negative events are usually described in a neutral tone. Further, business news employs genre-specific word usage; words seen as negative in “generic” contexts, may indicate a positive context here, and vice versa. Negative terms, e.g., include “cancer”, which in business often appears in positive contexts, as when pharmaceuticals unveil novel treatments. 

Dataset - 
We introduce a new dataset of over 17,000 manually labelled documents, which is substantially larger than any currently available resources. Despite being much larger than any existing datasets for business polarity detection, it is still small compared to what is typically used when training CNNs for text classification. 
The corpus is available at - puls.cs.helsinki.fi/ polarity 

ReadMe of dataset -

url The document source
content The document text
headline The headline position in the text
docnoId Unique identifier of the document
entities A list of annotated company names
entityId The entity identifier in this document
name Company name
offsets The entity position in the text
polarity Manually annotated polarity


Model description - 
In the preprocessing step we have extracted all the words corresponding to the given offsets, but not all of them are correct so we have used a similarity function which finds the similarity between the offset word and the name of the entity. If the similarity is above a given threshold, then we consider that word as a company keyword and replace it with a CTOK token. We have used one-hot encoding for the categorical labels i.e. polarities of the given data.
We have used a pretrained BERT model and then a single linear layer mapping to 5 output nodes. We have used the normal BERT model i.e., “bert-base-cased”. We used Pytorch-Lightning Library to implement training and testing as it is convenient compared to pytorch.
Note - Model is uploaded on Google drive and a link is provided in notebook itself to download.


Hyperparameters - 
Loss Function - BCEWithLogitsLoss
Optimizer - Adam (torch.optim.AdamW)
Learning Rate - 2e-5
Learning Rate Scheduler - get_linear_schedule_with_warmup
MAX_LEN = 512 words (BERT limitation)
