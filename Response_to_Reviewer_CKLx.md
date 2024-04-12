Thank you for your insightful comments!

$\S$ For detailed clarification of patterns and experimental results, please refer to [this link](http://bit.ly/49ADwMX).
### Q1 (CTS vs. MTS)：
CTS and MTS are related concepts, distinguished by their focus on interdependencies. MTS refers to data from multiple variables over time, while CTS, a subset of MTS, specifically highlights both temporal correlations within each series and spatial correlations among different series. Although all CTS are considered MTS, not all MTS demonstrate the explicit inter-series correlations required for CTS.
### Q2 (Irregular Sampling and No Ground Truth):
ReCTSi is engineered to handle both regularly and irregularly sampled datasets. For irregular sampling, adjustments include omitting the PST-pattern codebook tailored for regular intervals. Instead, we utilize the PT-codebook and PS-codebook mechanisms, which assign codes based on timestamp and node index information, irrespective of sampling frequency. Coupled with attention mechanisms that do not depend on temporal sequence, these adaptations ensure ReCTSi seamlessly accommodates irregularly sampled data.

Regarding the issue of unavailable ground truth, ReCTSi, as a supervised learning framework, is designed to tackle this challenge. During training, we simulate missing values by applying masks to valid data, creating pseudo-missing entries. The actual values of these entries act as ground truth for model supervision. 
### W1 (Clarification of Patterns)：
To elucidate the varied patterns within CTS, we use traffic flow as an illustrative example (see Fig. 2 and Lines 144-162). For a better clarification of patterns, we've now organized the information into a clearer format $\S$, accompanied by more detailed explanations.


Regarding the issue of unavailable GT, ReCTSi, as a supervised learning framework, is designed to tackle this challenge. During training, we simulate missing values by applying masks to valid data, creating pseudo-missing entries. The actual values of these entries act as GT for model supervision. 
### W2 (Most Challenging Pattern):
Our ablation study (see Tables 4, 6, and 7) examined the impact of removing pattern extraction modules from ReCTSi, aiming to identify which patterns are most critical for accuracy.

We found transient temporal and spatial patterns are most crucial, with their removal reducing accuracy substantially (30.44% for temporal and 20.03% for spatial patterns in MAE on AQ36). Besides, in the PPE phase, removing the PST-codebook significantly impacted accuracy, with a 12.13% decrease in MAE on AQ36. These insights indicate transient patterns' importance, a key consideration for low-resource settings. 
