# ArXiv Search Documentation

## summary

This is a arXiv search code that can help you search for any papers you want from arXiv API. 
Quote : “Thank you to arXiv for use of its open access interoperability.”

## Parameters 

|    Parameters     | Data Type |                            Usage                             |
| :---------------: | :-------: | :----------------------------------------------------------: |
|   search_query    |  string   | words user want to search for<br />note : if you want to search for two words and above, please this format instead: `quant+finance` or `web3+blockchain` |
|     search_by     |  string   |      user can search by `title`, `abstract`, `category`      |
| category_taxonomy |  string   | more taxonomy information can be found at : https://arxiv.org/category_taxonomy |
|      id_list      |  string   |              comma-delimited list of arXiv id's              |
|       start       |    int    | <br />type `-1 `to show all results<br />type `0` to show results from 0 - 9<br />type `1` to show results from 10 - 19<br />type `2` to show results from 20 - 29<br /> |
|    max_results    |    int    |  maximum number chucks of the results to download at a time  |

## Functions

##### `link go straight to each function use case`

| Functions                                                    | Explain                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [search without constrains](#search_without_constrains)      | simple arXiv search                                          |
| [search only by id_list](#search_only_by_id_list)            | search based on id_lsit and may only return one result       |
| [search by both search query and id_list](#search_by_both_search_query_and_id_list) | this may not generate any result since id_list could be unique |
| [search only by title](#search_only_by_title)                | search by papers title within different fields               |
| [search only by abstract](#search_only_by_abstract)          | looking for common words or related in the paper abstract section |
| [search only by category](#search_only_by_category)          | refer to [Parameters](#Parameters) `category_taxonomy` for more information |
| [search by both title and category](#search_by_both_title_and_category) | search papers by title within one typical field              |
| [search by both abstract and category](#search_by_both_abstract_and_category) | search papers by abstract within one typical field           |
| [view result in DataFrame](#view_result_in_DataFrame)       | this can help view result in DataFrame especially on Jupyter Notebook |

#### search_without_constrains

##### [ return back to `Functions` tables](#Functions)

```python
import arxiv_researchs as ar
# show all 2 results as `start = -1` and `max_results = 2`
raw_data = ar.arxiv_search(search_query = "quant", search_by = "", category_taxonomy = "", id_list = "", start = -1, max_results = 2)
result = ar.parse_xml_data(raw_data)
print(result)
```
```python
# exmaple output : 
{'paper_1': {'date published': '2023-09-19T23:50:45Z',
  'paper tile': 'Bell Correlations as Selection Artefacts',
  'category fields': 'quant-ph | physics.hist-ph',
  'paper summary': '  We propose an explanation of the correlations characteristic of Bell experiments, showing how they may arise as a special sort of selection artefact. This explanation accounts for the phenomena that have been taken to imply nonlocality, without recourse to any direct spacelike causality or influence. If correct, the proposal offers a novel way to reconcile nonlocality with relativity. The present paper updates an earlier version of the proposal (arXiv:2101.05370v4 [quant-ph], arXiv:2212.06986 [quant-ph]) in two main respects: (i) in demonstrating its application in a real Bell experiment; and (ii) in avoiding the need for an explicit postulate of retrocausality. ',
  'download link': 'http://arxiv.org/pdf/2309.10969v1'},
 'paper_2': {'date published': '2023-09-18T19:24:21Z',
  'paper tile': 'Reasoning about the Unseen for Efficient Outdoor Object Navigation',
  'category fields': 'cs.RO | cs.AI',
  'paper summary': '  Robots should exist anywhere humans do: indoors, outdoors, and even unmapped environments. In contrast, the focus of recent advancements in Object Goal Navigation(OGN) has targeted navigating in indoor environments by leveraging spatial and semantic cues that do not generalize outdoors. While these contributions provide valuable insights into indoor scenarios, the broader spectrum of real-world robotic applications often extends to outdoor settings. As we transition to the vast and complex terrains of outdoor environments, new challenges emerge. Unlike the structured layouts found indoors, outdoor environments lack clear spatial delineations and are riddled with inherent semantic ambiguities. Despite this, humans navigate with ease because we can reason about the unseen. We introduce a new task OUTDOOR, a new mechanism for Large Language Models (LLMs) to accurately hallucinate possible futures, and a new computationally aware success metric for pushing research forward in this more complex domain. Additionally, we show impressive results on both a simulated drone and physical quadruped in outdoor environments. Our agent has no premapping and our formalism outperforms naive LLM-based approaches ',
  'download link': 'http://arxiv.org/pdf/2309.10103v1'}}
```

#### search_only_by_id_list

##### [ return back to `Functions` tables](#Functions)

```python
import arxiv_researchs as ar
# show all 2 results as `start = -1` and `max_results = 2`
raw_data = ar.arxiv_search(search_query = "", search_by = "", category_taxonomy = "", id_list = "2301.04020v1", start = -1, max_results = 2)
result = ar.parse_xml_data(raw_data)
print(result)
```

```bash
# exmaple output : 
{'paper_1': {'date published': '2022-12-13T11:53:48Z',
  'paper tile': 'Quant 4.0: Engineering Quantitative Investment with Automated,\n  Explainable and Knowledge-driven Artificial Intelligence',
  'category fields': 'q-fin.CP | cs.AI',
  'paper summary': "  Quantitative investment (``quant'') is an interdisciplinary field combining financial engineering, computer science, mathematics, statistics, etc. Quant has become one of the mainstream investment methodologies over the past decades, and has experienced three generations: Quant 1.0, trading by mathematical modeling to discover mis-priced assets in markets; Quant 2.0, shifting quant research pipeline from small ``strategy workshops'' to large ``alpha factories''; Quant 3.0, applying deep learning techniques to discover complex nonlinear pricing rules. Despite its advantage in prediction, deep learning relies on extremely large data volume and labor-intensive tuning of ``black-box'' neural network models. To address these limitations, in this paper, we introduce Quant 4.0 and provide an engineering perspective for next-generation quant. Quant 4.0 has three key differentiating components. First, automated AI changes quant pipeline from traditional hand-craft modeling to the state-of-the-art automated modeling, practicing the philosophy of ``algorithm produces algorithm, model builds model, and eventually AI creates AI''. Second, explainable AI develops new techniques to better understand and interpret investment decisions made by machine learning black-boxes, and explains complicated and hidden risk exposures. Third, knowledge-driven AI is a supplement to data-driven AI such as deep learning and it incorporates prior knowledge into modeling to improve investment decision, in particular for quantitative value investing. Moreover, we discuss how to build a system that practices the Quant 4.0 concept. Finally, we propose ten challenging research problems for quant technology, and discuss potential solutions, research directions, and future trends. ",
  'download link': 'http://arxiv.org/pdf/2301.04020v1'}}
```

#### search_by_both_search_query_and_id_list

##### [ return back to `Functions` tables](#Functions)

```python
import arxiv_researchs as ar
# show all 2 results as `start = -1` and `max_results = 2`
raw_data = ar.arxiv_search(search_query = "quant", search_by = "", category_taxonomy = "", id_list = "2301.04020v1", start = -1, max_results = 2)
result = ar.parse_xml_data(raw_data)
result 
```

```bash
# exmaple output : 
{}
```

#### search_only_by_title

##### [ return back to `Functions` tables](#Functions)

```python
import arxiv_researchs as ar
# show all 2 results as `start = -1` and `max_results = 2`
raw_data = ar.arxiv_search(search_query = "quant", search_by = "title", category_taxonomy = "", id_list = "", start = -1, max_results = 2)
result = ar.parse_xml_data(raw_data)
print(result)
```

```bash
# exmaple output : 
{'paper_1': {'date published': '2023-08-02T04:06:16Z',
  'paper tile': 'QUANT: A Minimalist Interval Method for Time Series Classification',
  'category fields': 'cs.LG',
  'paper summary': "  We show that it is possible to achieve the same accuracy, on average, as the most accurate existing interval methods for time series classification on a standard set of benchmark datasets using a single type of feature (quantiles), fixed intervals, and an 'off the shelf' classifier. This distillation of interval-based approaches represents a fast and accurate method for time series classification, achieving state-of-the-art accuracy on the expanded set of 142 datasets in the UCR archive with a total compute time (training and inference) of less than 15 minutes using a single CPU core. ",
  'download link': 'http://arxiv.org/pdf/2308.00928v1'},
 'paper_2': {'date published': '2022-12-13T11:53:48Z',
  'paper tile': 'Quant 4.0: Engineering Quantitative Investment with Automated,\n  Explainable and Knowledge-driven Artificial Intelligence',
  'category fields': 'q-fin.CP | cs.AI',
  'paper summary': "  Quantitative investment (``quant'') is an interdisciplinary field combining financial engineering, computer science, mathematics, statistics, etc. Quant has become one of the mainstream investment methodologies over the past decades, and has experienced three generations: Quant 1.0, trading by mathematical modeling to discover mis-priced assets in markets; Quant 2.0, shifting quant research pipeline from small ``strategy workshops'' to large ``alpha factories''; Quant 3.0, applying deep learning techniques to discover complex nonlinear pricing rules. Despite its advantage in prediction, deep learning relies on extremely large data volume and labor-intensive tuning of ``black-box'' neural network models. To address these limitations, in this paper, we introduce Quant 4.0 and provide an engineering perspective for next-generation quant. Quant 4.0 has three key differentiating components. First, automated AI changes quant pipeline from traditional hand-craft modeling to the state-of-the-art automated modeling, practicing the philosophy of ``algorithm produces algorithm, model builds model, and eventually AI creates AI''. Second, explainable AI develops new techniques to better understand and interpret investment decisions made by machine learning black-boxes, and explains complicated and hidden risk exposures. Third, knowledge-driven AI is a supplement to data-driven AI such as deep learning and it incorporates prior knowledge into modeling to improve investment decision, in particular for quantitative value investing. Moreover, we discuss how to build a system that practices the Quant 4.0 concept. Finally, we propose ten challenging research problems for quant technology, and discuss potential solutions, research directions, and future trends. ",
  'download link': 'http://arxiv.org/pdf/2301.04020v1'}}
```

#### search_only_by_abstract

##### [ return back to `Functions` tables](#Functions)

```python
import arxiv_researchs as ar
# show all 2 results as `start = -1` and `max_results = 2`
raw_data = ar.arxiv_search(search_query = "quant", search_by = "abstract", category_taxonomy = "", id_list = "", start = -1, max_results = 2)
result = ar.parse_xml_data(raw_data)
print(result)
```

```bash
# exmaple output : 
{'paper_1': {'date published': '2023-09-19T23:50:45Z',
  'paper tile': 'Bell Correlations as Selection Artefacts',
  'category fields': 'quant-ph | physics.hist-ph',
  'paper summary': '  We propose an explanation of the correlations characteristic of Bell experiments, showing how they may arise as a special sort of selection artefact. This explanation accounts for the phenomena that have been taken to imply nonlocality, without recourse to any direct spacelike causality or influence. If correct, the proposal offers a novel way to reconcile nonlocality with relativity. The present paper updates an earlier version of the proposal (arXiv:2101.05370v4 [quant-ph], arXiv:2212.06986 [quant-ph]) in two main respects: (i) in demonstrating its application in a real Bell experiment; and (ii) in avoiding the need for an explicit postulate of retrocausality. ',
  'download link': 'http://arxiv.org/pdf/2309.10969v1'},
 'paper_2': {'date published': '2023-09-08T09:58:25Z',
  'paper tile': 'Interband scattering- and nematicity-induced quantum oscillation\n  frequency in FeSe',
  'category fields': 'cond-mat.str-el | cond-mat.dis-nn | cond-mat.supr-con',
  'paper summary': '  Understanding the nematic phase observed in the iron-chalcogenide materials is crucial for describing their superconducting pairing. Experiments on FeSe$_{1-x}$S$_x$ showed that one of the slow Shubnikov--de Haas quantum oscillation frequencies disappears when tuning the material out of the nematic phase via chemical substitution or pressure, which has been interpreted as a Lifshitz transition [Coldea et al., npj Quant Mater 4, 2 (2019), Reiss et al., Nat. Phys. 16, 89-94 (2020)]. Here, we present a generic, alternative scenario for a nematicity-induced sharp quantum oscillation frequency which disappears in the tetragonal phase and is not connected to an underlying Fermi surface pocket. We show that different microscopic interband scattering mechanisms - for example, orbital-selective scattering - in conjunction with nematic order can give rise to this quantum oscillation frequency beyond the standard Onsager relation. We discuss implications for iron-chalcogenides and the interpretation of quantum oscillations in other correlated materials. ',
  'download link': 'http://arxiv.org/pdf/2309.04237v1'}}
```

#### search_only_by_category

##### [ return back to `Functions` tables](#Functions)

```python
import arxiv_researchs as ar
# show all 2 results as `start = -1` and `max_results = 2`
raw_data = ar.arxiv_search(search_query = "", search_by = "category", category_taxonomy = "q-fin.CP", id_list = "", start = -1, max_results = 2)
result = ar.parse_xml_data(raw_data)
print(result)
```

```bash
# exmaple output :
{'paper_1': {'date published': '2023-09-21T11:26:36Z',
  'paper tile': 'Stock Market Sentiment Classification and Backtesting via Fine-tuned\n  BERT',
  'category fields': 'q-fin.CP | cs.CL | cs.LG',
  'paper summary': '  With the rapid development of big data and computing devices, low-latency automatic trading platforms based on real-time information acquisition have become the main components of the stock trading market, so the topic of quantitative trading has received widespread attention. And for non-strongly efficient trading markets, human emotions and expectations always dominate market trends and trading decisions. Therefore, this paper starts from the theory of emotion, taking East Money as an example, crawling user comment titles data from its corresponding stock bar and performing data cleaning. Subsequently, a natural language processing model BERT was constructed, and the BERT model was fine-tuned using existing annotated data sets. The experimental results show that the fine-tuned model has different degrees of performance improvement compared to the original model and the baseline model. Subsequently, based on the above model, the user comment data crawled is labeled with emotional polarity, and the obtained label information is combined with the Alpha191 model to participate in regression, and significant regression results are obtained. Subsequently, the regression model is used to predict the average price change for the next five days, and use it as a signal to guide automatic trading. The experimental results show that the incorporation of emotional factors increased the return rate by 73.8\\% compared to the baseline during the trading period, and by 32.41\\% compared to the original alpha191 model. Finally, we discuss the advantages and disadvantages of incorporating emotional factors into quantitative trading, and give possible directions for further research in the future. ',
  'download link': 'http://arxiv.org/pdf/2309.11979v1'},
 'paper_2': {'date published': '2023-09-21T10:30:49Z',
  'paper tile': 'A Comprehensive Review on Financial Explainable AI',
  'category fields': 'cs.AI | cs.CE | q-fin.CP',
  'paper summary': '  The success of artificial intelligence (AI), and deep learning models in particular, has led to their widespread adoption across various industries due to their ability to process huge amounts of data and learn complex patterns. However, due to their lack of explainability, there are significant concerns regarding their use in critical sectors, such as finance and healthcare, where decision-making transparency is of paramount importance. In this paper, we provide a comparative survey of methods that aim to improve the explainability of deep learning models within the context of finance. We categorize the collection of explainable AI methods according to their corresponding characteristics, and we review the concerns and challenges of adopting explainable AI methods, together with future directions we deemed appropriate and important. ',
  'download link': 'http://arxiv.org/pdf/2309.11960v1'}}
```

#### search_by_both_title_and_category

##### [ return back to `Functions` tables](#Functions)

```python
import arxiv_researchs as ar
# show all 2 results as `start = -1` and `max_results = 2`
raw_data = ar.arxiv_search(search_query = "quant", search_by = "title", category_taxonomy = "q-fin.CP", id_list = "", start = -1, max_results = 2)
result = ar.parse_xml_data(raw_data)
print(result)
```

```bash
# exmaple output :
{'paper_1': {'date published': '2022-12-13T11:53:48Z',
  'paper tile': 'Quant 4.0: Engineering Quantitative Investment with Automated,\n  Explainable and Knowledge-driven Artificial Intelligence',
  'category fields': 'q-fin.CP | cs.AI',
  'paper summary': "  Quantitative investment (``quant'') is an interdisciplinary field combining financial engineering, computer science, mathematics, statistics, etc. Quant has become one of the mainstream investment methodologies over the past decades, and has experienced three generations: Quant 1.0, trading by mathematical modeling to discover mis-priced assets in markets; Quant 2.0, shifting quant research pipeline from small ``strategy workshops'' to large ``alpha factories''; Quant 3.0, applying deep learning techniques to discover complex nonlinear pricing rules. Despite its advantage in prediction, deep learning relies on extremely large data volume and labor-intensive tuning of ``black-box'' neural network models. To address these limitations, in this paper, we introduce Quant 4.0 and provide an engineering perspective for next-generation quant. Quant 4.0 has three key differentiating components. First, automated AI changes quant pipeline from traditional hand-craft modeling to the state-of-the-art automated modeling, practicing the philosophy of ``algorithm produces algorithm, model builds model, and eventually AI creates AI''. Second, explainable AI develops new techniques to better understand and interpret investment decisions made by machine learning black-boxes, and explains complicated and hidden risk exposures. Third, knowledge-driven AI is a supplement to data-driven AI such as deep learning and it incorporates prior knowledge into modeling to improve investment decision, in particular for quantitative value investing. Moreover, we discuss how to build a system that practices the Quant 4.0 concept. Finally, we propose ten challenging research problems for quant technology, and discuss potential solutions, research directions, and future trends. ",
  'download link': 'http://arxiv.org/pdf/2301.04020v1'},
 'paper_2': {'date published': '2019-11-27T15:45:06Z',
  'paper tile': 'Introduction to Solving Quant Finance Problems with Time-Stepped FBSDE\n  and Deep Learning',
  'category fields': 'q-fin.CP | cs.CE | q-fin.MF | q-fin.PR',
  'paper summary': '  In this introductory paper, we discuss how quantitative finance problems under some common risk factor dynamics for some common instruments and approaches can be formulated as time-continuous or time-discrete forward-backward stochastic differential equations (FBSDE) final-value or control problems, how these final value problems can be turned into control problems, how time-continuous problems can be turned into time-discrete problems, and how the forward and backward stochastic differential equations (SDE) can be time-stepped. We obtain both forward and backward time-stepped time-discrete stochastic control problems (where forward and backward indicate in which direction the Y SDE is time-stepped) that we will solve with optimization approaches using deep neural networks for the controls and stochastic gradient and other deep learning methods for the actual optimization/learning. We close with examples for the forward and backward methods for an European option pricing problem. Several methods and approaches are new. ',
  'download link': 'http://arxiv.org/pdf/1911.12231v1'}}
```

#### search_by_both_abstract_and_category

##### [ return back to `Functions` tables](#Functions)

```python
import arxiv_researchs as ar
# show all 2 results as `start = -1` and `max_results = 2`
raw_data = ar.arxiv_search(search_query = "quant", search_by = "abstract", category_taxonomy = "q-fin.CP", id_list = "", start = -1, max_results = 2)
result = ar.parse_xml_data(raw_data)
print(result)
```

```bash
# exmaple output :
{'paper_1': {'date published': '2023-07-31T16:40:06Z',
  'paper tile': 'Alpha-GPT: Human-AI Interactive Alpha Mining for Quantitative Investment',
  'category fields': 'q-fin.CP | cs.AI | cs.CL',
  'paper summary': "  One of the most important tasks in quantitative investment research is mining new alphas (effective trading signals or factors). Traditional alpha mining methods, either hand-crafted factor synthesizing or algorithmic factor mining (e.g., search with genetic programming), have inherent limitations, especially in implementing the ideas of quants. In this work, we propose a new alpha mining paradigm by introducing human-AI interaction, and a novel prompt engineering algorithmic framework to implement this paradigm by leveraging the power of large language models. Moreover, we develop Alpha-GPT, a new interactive alpha mining system framework that provides a heuristic way to ``understand'' the ideas of quant researchers and outputs creative, insightful, and effective alphas. We demonstrate the effectiveness and advantage of Alpha-GPT via a number of alpha mining experiments. ",
  'download link': 'http://arxiv.org/pdf/2308.00016v1'},
 'paper_2': {'date published': '2022-12-13T11:53:48Z',
  'paper tile': 'Quant 4.0: Engineering Quantitative Investment with Automated,\n  Explainable and Knowledge-driven Artificial Intelligence',
  'category fields': 'q-fin.CP | cs.AI',
  'paper summary': "  Quantitative investment (``quant'') is an interdisciplinary field combining financial engineering, computer science, mathematics, statistics, etc. Quant has become one of the mainstream investment methodologies over the past decades, and has experienced three generations: Quant 1.0, trading by mathematical modeling to discover mis-priced assets in markets; Quant 2.0, shifting quant research pipeline from small ``strategy workshops'' to large ``alpha factories''; Quant 3.0, applying deep learning techniques to discover complex nonlinear pricing rules. Despite its advantage in prediction, deep learning relies on extremely large data volume and labor-intensive tuning of ``black-box'' neural network models. To address these limitations, in this paper, we introduce Quant 4.0 and provide an engineering perspective for next-generation quant. Quant 4.0 has three key differentiating components. First, automated AI changes quant pipeline from traditional hand-craft modeling to the state-of-the-art automated modeling, practicing the philosophy of ``algorithm produces algorithm, model builds model, and eventually AI creates AI''. Second, explainable AI develops new techniques to better understand and interpret investment decisions made by machine learning black-boxes, and explains complicated and hidden risk exposures. Third, knowledge-driven AI is a supplement to data-driven AI such as deep learning and it incorporates prior knowledge into modeling to improve investment decision, in particular for quantitative value investing. Moreover, we discuss how to build a system that practices the Quant 4.0 concept. Finally, we propose ten challenging research problems for quant technology, and discuss potential solutions, research directions, and future trends. ",
  'download link': 'http://arxiv.org/pdf/2301.04020v1'}}
```

#### view_result_in_DataFrame 

##### [ return back to `Functions` tables](#Functions)

```python
import arxiv_researchs as ar
# show all 2 results as `start = -1` and `max_results = 2`
raw_data = ar.arxiv_search(search_query = "quant", search_by = "abstract", category_taxonomy = "q-fin.CP", id_list = "", start = -1, max_results = 2)
result = ar.parse_xml_data(raw_data)

# make download link clickable
def make_clickable(val):
    # target _blank to open new window
    return '<a target="_blank" href="{}">{}</a>'.format(val,val)
  
# view DataFrame results
view_df =  ar.view_dataframe(result)
view_df.style.format({'paper_download_link': make_clickable})
```

![view_df_pic](https://github.com/codemakerss/arXiv_search/blob/main/sreenshots/view_df.png)



