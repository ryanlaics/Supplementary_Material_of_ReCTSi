Review:
The work introduces a method for imputing correlated time series data through a two-phase architecture. The first phase, Persistent Pattern Extraction, employs a Multi-view Learnable Codebook to identify and archive common persistent patterns across different time series for quick retrieval during inference. The second phase, Transient Pattern Adaptation, uses completeness-aware attention modules to focus on complete and reliable data segments, capturing transient patterns influenced by data dynamics, drifts, or anomalies.

Pros:

1- Efficiency and Resource Conservation

2- Enhanced Imputation Accuracy

Cons:

Potential Overfitting Risks and the Dependency on Data Quality

Questions:
1- Could you elaborate on how scalable the ReCTSi framework is when applied to datasets with a very large number of sensors or channels?

2- Detailed sensitivity analysis for the framework hyperparameters is lacking. Could you provide insights into how the hyperparameters were optimized across different datasets?

3- In the context of using a learnable codebook for pattern extraction, can you discuss the model's ability to capture long-term dependencies within the data?

4- Would it be possible to include a detailed case study or example in your paper illustrating how ReCTSi captures and utilizes PT-patterns, PS-patterns, etc, in a practical scenario?

Ethics Review Flag: No
Ethics Review Description: no
Scope: 4: The work is relevant to the Research track of KDD and is of broad interest to the community
Novelty: 4: Average
Technical Quality: 4: Average
Presentation Quality: 2: Average (it needs some effort to understand, but it should be ok after some editing)
Reproducibility: 3: Excellent (it provides sufficient details, and the code and data are accessible)
Reviewer Confidence: 3: The reviewer is confident but not certain that the evaluation is correct

----------------------------------
Thanks for your time and comments.

$^\S$For detailed clarification of patterns and experimental results, please refer to [this link](http://bit.ly/49ADwMX).
### Q1 (Scalability):
In line with the conventions of recent SOTA methods like PoGeVon and GRIN, we initially utilized the AQ36 dataset for evaluation. Following your suggestion, we extended our experiments to the larger air quality dataset, AQ437, from which AQ36 is derived$^\S$. The results affirm ReCTSi's capability to effectively handle datasets with a large sensor count, achieving superior accuracy (MAE: 23.574). Notably, PoGeVon, the second most accurate model on AQ36, encountered the out-of-memory issue on an Nvidia Quadro RTX 8000 GPU and could not be evaluated on AQ437, where other baselines also showed less accuracy (MAE not lower than 29.582).
### Q2 (Hyperparameter):
Within ReCTSi, there are four main hyperparameters: embedding size, window size, CaA block number, and total codebook size. In the original submission, we have presented the hyperparameter studies of the most important hyperparameters: embedding size and window size in Fig.5. 

Besides, through extensive experiments, we suggest limiting the CaA block number to one or two for optimal performance in the caption of Figure 3. We have added the additional hyper-parameter study of the CaA block number$^\S$, with one block yielding an MAE of 19.48 on AQ36. Increasing the CaA block number to two or three resulted in higher MAEs of 21.23 and 26.64, respectively. Regarding the total codebook size, our findings indicate a relative insensitivity due to the PCF's compression capabilities. Even with larger codebook sizes, the model maintains stable accuracy (MAE ranging from 19.483 to 20.659 with total codebook size from 24 to 120 on AQ36), as redundant information is efficiently condensed.

Based on these results, we recommend an embedding size comparable to the dataset's channel count for adequate expressiveness and suggest limiting CaA blocks to one or two. A larger initial codebook size is advisable, with PCF ensuring efficient compression. These practical guidelines for configuring ReCTSi will be included in the final version.
### Q3 (Ability to Capture Long-term Dependencies):
ReCTSi's use of the learnable codebook mechanism in the TPA phase incorporates attention modules specifically chosen for their adeptness at capturing long-term dependencies. Inspired by the efficacy of transformer (i.e., self-attention mechanisms) in managing long-range dependencies within large language models, these modules ensure ReCTSi excels in identifying and leveraging complex temporal relationships over extended periods. This strategic integration of attention-based modules into ReCTSi highlights our commitment to utilizing advanced techniques for profound long-term pattern recognition in time series data.

### Q4 (Multiple Patterns):
To elucidate the varied patterns within CTS, we use traffic flow as an illustrative example (see Fig. 2 and Lines 144-162). For a better clarification of patterns, we've now organized the information into a clearer format for your reference$^\S$, accompanied by detailed explanations.

### W1 (Overfitting Risks and Dependency on Data Quality):
ReCTSi’s minimal parameter count, significantly lower than baseline models (76K for ReCTSi vs. 191K for the nearest competitor, GRIN), inherently reduces overfitting risks. Besides, ReCTSi is evaluated across various domains, including traffic, air quality, and COVID-19, exhibits SOTA accuracy and efficiency. This underscores its generalizability across different data quality scenarios.
