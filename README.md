LibRec
======

[![Join the chat at https://gitter.im/librec/Lobby](https://badges.gitter.im/librec/Lobby.svg)](https://gitter.im/librec/Lobby?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

**LibRec** (http://www.librec.net) is a Java library for recommender systems (Java version 1.7 or higher required). It implements a suit of state-of-the-art recommendation algorithms, aiming to resolve two classic recommendation tasks: **rating prediction** and **item ranking**. 

### Authors Words about the NEW Version
First of all, LibRec 2.0 is COMING, and will be released in the December 2016. It has been a year since the last version was released. In this year, lots of changes have been taken to the LibRec project, and the most significant one is the formulation of the LibRec team. The team pushes forward the development of LibRec with the wisdom of many experts, and the collaboration of experienced and enthusiastic contributors. Without their great efforts and hardworking, it is impossible to reach the state that a single developer may dream for. 

LibRec 2.0 is not the end of our teamwork, but just the begining of greater objectives. We aim to continously provide NEXT versions for better experience and performance. There are many directions and goals in plan, and we will do our best to make them happen. It is always exciting to receive any code contributions, suggestions, comments from all our LibRec users. 

We hope you will enjoy the new version!

![LibRec Structure](http://www.librec.net/images/librec.png)

### Features

* **Rich Algorithms:** More than 70 recommendation algorithms have been implemented, and more will be added in the LibRec.
* **Module Composition:** LibRec has six main components including data split, conversion, similarity, algorithms, evaluators and filters.
* **Flexible Configuration:** LibRec is based on low coupling, flexible and either external textual or internal API configuration.. 
* **High Performance:** LibRec has more efficient implementations than other counterparts while producing comparable accuracy.
* **Simple Usage:** LibRec can get executed in a few lines of codes, and a number of demos are provided for easy start.
* **Easy Expansion:** LibRec provides a set of recommendation interfaces for easy expansion to implement new recommenders.

### Download
* **librec-v2.0** is coming soon!
   * Alpha version: check out the new branch (2.0.0-alpha) 
      * Note that this update is not a stable release, and bugs and issues may exist here and there for now. This version is suitable for those who seek for the latest update and changes in LibRec 2.0. The stable version will be available by the end of December 2016. 
   * Beta version by the middle of December 2016
   * Full version by the end of December 2016
* **[librec-v1.3](http://www.librec.net/release/librec-v1.3.zip)**
* **[librec-v1.2](http://www.librec.net/release/librec-v1.2.zip)**
* **[librec-v1.1](http://www.librec.net/release/librec-v1.1.zip)**
* **[librec-v1.0](http://www.librec.net/release/librec-v1.0.zip)**


### Code Snippet

You can use **LibRec** as a part of your projects, and use the following codes to run a recommender. 

<pre>
public void main(String[] args) throws Exception {
	
	// recommender configuration
	Configuration conf = new Configuration();
	Resource resource = new Resource("rec/cf/userknn-test.properties");
	conf.addResource(resource);

	// build data model
	DataModel dataModel = new TextDataModel(conf);
	dataModel.buildDataModel();
	
	// set recommendation context
	RecommenderContext context = new RecommenderContext(conf, dataModel);
	RecommenderSimilarity similarity = new PCCSimilarity();
	similarity.buildSimilarityMatrix(dataModel, true);
	context.setSimilarity(similarity);

	// training
	Recommender recommender = new UserKNNRecommender();
	recommender.recommend(context);

	// evaluation
	RecommenderEvaluator evaluator = new MAEEvaluator();
	recommender.evaluate(evaluator);

	// recommendation results
	List<RecommendedItem> recommendedItemList = recommender.getRecommendedList();
	RecommendedFilter filter = new GenericRecommendedFilter();
	recommendedItemList = filter.filter(recommendedItemList);
}
</pre>

### Reference
Please cite the following papers if LibRec is helpful to your research. 

1. Guibing Guo, Jie Zhang, Zhu Sun and Neil Yorke-Smith, [LibRec: A Java Library for Recommender Systems](http://ceur-ws.org/Vol-1388/demo_paper1.pdf), in Posters, Demos, Late-breaking Results and Workshop Proceedings of the 23rd Conference on User Modelling, Adaptation and Personalization (UMAP), 2015.

### Acknowledgement

We would like to express our appreciation to the following people for contributing source codes to LibRec, including [Prof. Robin Burke](http://josquin.cti.depaul.edu/~rburke/), [Bin Wu](https://github.com/wubin7019088), [Ge Zhou](https://github.com/466152112), [Ran Locar](https://github.com/ranlocar), [Shawn Rutledge](https://github.com/shawndr), [Tao Lian](https://github.com/taolian), [Takuya Kitazawa](https://github.com/takuti), etc. 

We also appreciate many others for reporting bugs and issues, and for providing valuable suggestions and support. 

### Publications
LibRec has been used in the following publications (let me know if your paper is not listed):

1. G. Guo, J. Zhang and N. Yorke-Smith, TrustSVD: Collaborative Filtering with Both the Explicit and Implicit Influence of User Trust and of Item Ratings, in Proceedings of the 29th AAAI Conference on Artificial Intelligence (AAAI), 2015, 123-129.
2. Z. Sun, G. Guo and J. Zhang, Exploiting Implicit Item Relationships for Recommender Systems, in Proceedings of the 23rd International Conference on User Modeling, Adaptation and Personalization (UMAP), 2015.


### GPL License

LibRec is [free software](http://www.gnu.org/philosophy/free-sw.html): you can redistribute it and/or modify it under the terms of the [GNU General Public License (GPL)](http://www.gnu.org/licenses/gpl.html) as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version. LibRec is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details. 

You should have received a copy of the GNU General Public License along with LibRec. If not, see http://www.gnu.org/licenses/.
