# French News for lazy butts

#### Setup

Few points to remember

* We will be using the git branching model according to [this](http://jeffkreeftmeijer.com/2010/why-arent-you-using-git-flow/)
  * There is a [git plugin](https://github.com/nvie/gitflow) for the same.
  * It is important that we branch from the branch develop (always), not doing so could cause merge conflicts.
  * Only tested code would be pushed to master.
  * When merging features to develop please create a pull request and then merge. This will help us in roling back the changes.
* For first time git users, please use a git GUI like sourcetree. 

***


#### Scrapping 
* Things that require a change:
  * page no
  * MAX_PAGE_NO
  * name of the spider
* Follow the convention i have follwed , ie lemonde-fr-spiderurl
* You have to go to the website, enter your search string and copy the url, also note the max pages to be iterated.
then parse is responsible for parsing html pages
* You need to extract the links ie anchor tags by giving the genral xpath
* Follow scrapy tutorial for more details

***

### Proposal

#### Introduction
The limitation of time caters to the reluctance of many individuals to read long-winded news articles. In the current scenario where headlines are misleading we need a synoptic view of an article.


Motivated by the aforementioned reasons, we propose an application that encapsulates daily news in French in 60 words. We will use an encoder-decoder recurrent neural network with LSTM units to generate abstractive summaries from text of multiple news articles. Abstractive summarization is an elusive technological capability in which textual summaries of content are generated de novo (Fei Liu et al., 2015).


Although, many deep learning methods have been proposed to summarise news articles in english, fewer strategies exist to concisely and coherently paraphrase news article in french.

#### Method
##### Materials
The proposed model will be trained using the wikinews french article dataset and a self scraped corpus from french news websites like www.lemonde.fr, www.lesechos.fr, www.ouest-france.fr,  all of which will account to approximately 1 million articles. Since the proposed approach uses unsupervised learning, the dataset will not require any reference summaries.


The data obtained will be formatted as follows:
* Tags / Domain / Category
* News content

##### Procedure
We plan to implement a sequence to sequence learning model which consists of 2 recurrent neural networks with long short term memory (LSTM) units. The first LSTM is an encoder that takes as input a news article to build a large dimensional vector representation and the second LSTM is a decoder that takes the encoder’s output and generates a summary of up to 60 words. We then use beam search to select the most suitable headline out of all candidate headlines generated by the model. Moreover, we do not need to define explicit features as our model will learn features on its own.


We will use Tensorflow's python library to implement the proposed sequence to sequence model.


##### Evaluation
In order to evaluate the performance of the summarizer, we will use FRESA which is capable of evaluating the generated summaries without reference summaries. FRESA is similar to ROUGE and works by calculating the divergence of the generated summary and the original article. In this case, we will be using the Kullback-Leibler (KL) divergence with Dirichlet smoothing for evaluation (Saggion et al., 2010).

***

PS: If I missed out something please add.