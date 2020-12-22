# Council on Foreign Relations Nigeria Security Tracker

This is an evolving and experimental respository of machine learning models to support the collection and coding of incidents of political violence that underpin the [Council on Foreign Relations Nigeria Security Tracker.](https://www.cfr.org/nigeria/nigeria-security-tracker/p29483)

Currently, data collection and coding is a manual process. We use a collection of RSS feeds to collect as many potentially relevant articles as possible. We then apply a series of search terms to filter out irrelevant articles. A human coder then manually parses news articles to identify incidents and enters that information into a spreadsheet.

We began prototyping computer-assisted incident identification as far back as 2013, when we partnered with a team of graduate students from Columbia University to build a prototype to collect data about social unrest in South Africa. At the time, the necessary technology was just not in a place where it was easily accessible AND accurate enough to deliver useful results.

Jump forwad to 2016, when we achieved some modest success by applying bag of words and logistic regression to identify, for example, what state in Nigeria an event took place. However, our overall accuracy scores were still in the low 70 percents, and majorly imbalanced classes (disproportionate number of incidents occur in northeastern nigeria, for example) impacted the usefulness of these models.

Since then, natural language processing and machine classification has advanced significantly--from the speed afforded by much more powerful computers to process text and train models, to a major shift in techniques, from bag of words to word embedding, from logistic regression (which still does pretty well) to neural networks as well as cloud services and web frameworks that simplify putting these models into production.

## Boko Haram Model

This model reads in an article and predicts whether the article is discussing an incident in which Boko Haram is involved with 88 percent test accuracy. While this sounds like a relatively easy challenge to solve, early iterations only achieved at best 68 percent accuracy. This early poor performance is related to the small size of the dataset I had to work with -- roughly 10,000 articles -- and that only about 3,000 of those articles reference incidents involving Boko Haram. As a result of this highly imbalanced data, the models tended to predict the dominant "not Boko Haram" class almost everytime. 

I was able to solve this problem by augmenting the dataset with synthetic data. Using the `textaugment` package, I synthesized roughly 40,000 additional articles, and then withheld the original "real data" as my test set. This means that even though the model was trained almost entirely on synthetic data, it was still able to deliver acceptable accuracy. More importantly, even though my test set was imbalanced, with only 3000 "boko haram" samples to 6000 "not boko haram" samples, I was able to achieve an acceptable precision score of .76 and recall of .95 for the "boko haram" class. 

To explore the model more:

[Text augmentation code](https://github.com/AschHarwood/nigeria_security_tracker_models_cfr/blob/main/notebooks/preprocessing/data_augmentation_bh_12_19_20_final.ipynb)

[Model code](https://github.com/AschHarwood/nigeria_security_tracker_models_cfr/blob/main/notebooks/model/nn_boko_haram_v2_acled_expanded_nst_final_12_19_20.ipynb)

[Download the model](https://drive.google.com/drive/folders/1FCgwH5QL6gKubTeRE1fmzvNAuCxdWtOp?usp=sharing)

[Download the real and synthetic datasets](https://github.com/AschHarwood/nigeria_security_tracker_models_cfr/tree/main/notebooks/data)

## Next Steps

The long term goal is to develop a suite of models and put them into a pipeline that will allow quasi-realtime monitoring of political violence in Nigeria. In short term, I will first focus on modeling "perpetrator" classification, then followed by date and location classication. Assuming acceptable performance across these key metrics, the next step would be to move from simple article classification to acutal incident identification. 
