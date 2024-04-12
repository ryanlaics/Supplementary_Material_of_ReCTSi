Review:
Summary
ReCTSi introduces an approach for the imputation of Correlated Time Series (CTS). ReCTSi presents a two-phase architecture aimed at efficient pattern learning. The first phase employs a multi-view learnable codebook to identify, archive, and swiftly retrieve common patterns across time series. The second phase, Transient Pattern Adaptation, leverages completeness-aware attention modules to prioritize complete, reliable data segments for imputation. Through testing, ReCTSi sets a new standard in imputation accuracy and reduces computational requirements.

Strength
The overall presentation flow is easy to follow, good and informative visualizations (fig 3, 4).
The proposed ReCTSi framework yields better performance gap for CTS imputation task, while being efficient both in memory and time.
Weakness
The same notation of t in Eq.(4), (6) might cause confusion.
In the design of completeness matrix, the authors assume the data segments containing missing values contribute less to pattern learning. I wonder if this assumption hold true in most cases. For both temporal or spatial dependence, the widely used assumption is that the closer neighbors should be more related to the data point of interest. How does ReCTSi handle those cases when completeness matrix reduces the weight of nearby neighborhood?
What is the rationale of using Grouped Feedforward Network instead of ordinary Feedforward Network to make final inference?
Questions:
Please refer to weaknesses mentioned above.

Ethics Review Flag: No
Ethics Review Description: n/a
Scope: 3: The work is somewhat relevant to the Research track of KDD and is of narrow interest to a sub-community
Novelty: 5: Above Average
Technical Quality: 5: Above Average
Presentation Quality: 3: Excellent (it is a pleasure to read and easy to understand, it has good figures and insightful explanations)
Reproducibility: 3: Excellent (it provides sufficient details, and the code and data are accessible)
Reviewer Confidence: 3: The reviewer is confident but not certain that the evaluation is correct

----------------------------------
Thanks for your time and comments.

$^\S$For detailed visualizations of CaA and experimental results, please refer to [this link](http://bit.ly/49ADwMX).
### Q1 (Confusion of the Same Notation t):
Thanks! We'll use different notations in Eq. (4) and (6) to express their timestamp indices in the final version.
### Q2 (Assumption of CaA):
In CaA, the self-attention mechanism can address the long-term dependancy issue, where the features from either neighbor or distant segments can be processed equally in CaA. However, the vanilla self-attention mechanism lacks considering data reliability (which is indicated by the completeness of data segment). ReCTSi’s CaA leverages the self-attention mechanism to evaluate both nearby and distant data segments, **focusing on their informational completeness rather than just proximity**. This is crucial because, in cases where a neighboring segment is largely missing, its contribution to understanding the current data point is minimal, rendering it less reliable. Conversely, a distant segment with complete data can offer valuable insights, deserving a higher weight in the analysis$^\S$. Thus, our CaA allows for better tradeoff between the temporal position impact and data completeness.
### Q3 (Rationale of Using Grouped FFN):
In fact, we have explored various methods to reduce the complexity in the TPA's attention modules, including adopting advanced transformer variants during ReCTSi's design. Despite these efforts, we found that existing alternatives led to accuracy losses for the imputation task (e.g., ReCTSi-Informer variant adopt the efficient attention mechanism from Informer, presents about 50% FLOPs decrease, while leading to 36% accuracy loss$^\S$, which is not acceptable). Consequently, motivated by Group Convolution, we then formulated the Grouped FFN mechanism. This adoption balances efficiency with effectiveness, avoiding the accuracy compromises observed in previous iterations. 
