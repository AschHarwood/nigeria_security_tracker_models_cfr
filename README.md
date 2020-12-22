# Council on Foreign Relations Nigeria Security Tracker

This is an evolving respository of machine learning models to support the collection and coding of incidents of political violence that underpin the [Council on Foreign Relations Nigeria Security Tracker.](https://www.cfr.org/nigeria/nigeria-security-tracker/p29483)

Currently, data collection and coding is a manual process. We use a collection of RSS feeds to collect as many potentially relevant articles as possible. We then apply a series of search terms to filter out irrelevant articles. A human coder then manually parse news articles to identify incidents and enters that information into a spreadsheet.

We began prototyping computer-assisted incident and identification coding as far back as 2013, when we partnered with a team of graduate students from Columbia University to build a prototype to collect data about social unrest and protest in South Africa. At the time, the necessary technology was just not in a place where it was easily accessible AND accurate enough to deliver useful results.

Jump forwad to 2016, when we achieved some modest success by applying bag of words and logistic regression to identify, for example, what state in Nigeria an event took place. However, our overall accuracy scores were still in the low 70 percents, and majorly imbalanced classes (disproportionate number of incidents occur in northeastern nigeria, for example) impacted the usefulness of these models.

Since then, natural language processing and machine classification has advanced significantly--from the speed afforded by much more powerful computers to process text and train models, to a major shift in techniques, from bag of words to word embedding, from logistic regression (which still does pretty well) to neural networks as well as cloud services and web frameworks that simplify putting these models into production.
