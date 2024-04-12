Review:

The paper, titled “ReCTSi: Resource-efficient Correlated Time Series Imputation via Decoupled Pattern Learning and Completeness-aware Attentions,” discusses a method for imputing missing data in correlated time series (CTS) efficiently. The paper introduces ReCTSi, a method that significantly reduces computational resources for CTS imputation while maintaining high accuracy. ReCTSi employs a two-phase architecture: Persistent Pattern Extraction (PPE) and Transient Pattern Adaptation (TPA). PPE identifies common patterns across time series, while TPA focuses on adapting to the complete and reliable segments of data. The method includes a novel attention mechanism that prioritizes complete data segments during the imputation process, which is crucial for handling CTS data's dynamic and incomplete nature.

Pros

ReCTSi significantly reduces computational resources for time series imputation while maintaining high accuracy. This makes it suitable for resource-limited scenarios, such as edge computing.
The two-phase architecture (Persistent Pattern Extraction and Transient Pattern Adaptation) allows ReCTSi to identify common patterns across time series and adapt to reliable data segments.
The novel completeness-aware attention mechanism prioritizes complete data segments during imputation, which is crucial for handling dynamic and incomplete time series data.
ReCTSi achieves state-of-the-art imputation accuracy with significantly fewer computational resources than existing models.
Cons

The model’s architecture involves multiple components (e.g., MvLC, PCF) and hyperparameters. Implementing and fine-tuning these components may require expertise.
While ReCTSi performs well across various domains (traffic flow, air quality, COVID-19), its effectiveness may vary depending on the specific dataset characteristics.
Balancing accuracy and resource efficiency is challenging. Some applications may prioritize accuracy over resource savings, and vice versa.
Overall, ReCTSi offers an innovative approach to time series imputation, but its adoption should consider the trade-offs between accuracy, complexity, and resource constraints.

Questions:
For the COVID-19 dataset, the number of timestamps is rather small, so we expected the traditional non-DL methods (MEAN, MF, MICE) to be more accurate than DL-based methods, but the results show the opposite. How can we explain this phenomenon?
Are there specific scenarios where traditional methods still outperform ReCTSi?
While ReCTSi performs well across various domains(traffic, air quality, and infection), are there plans to extend ReCTSi to handle other types of time series data (e.g., financial data, sensors)? Can we guarantee that the ReCTSi still shows high accuracy compared to other methods?
The attention mechanism in ReCTSi prioritizes complete data segments. Could you provide insights into how this mechanism works through visualizations and whether it can be further fine-tuned or customized for specific applications?
How does it perform in scenarios with noisy or irregularly sampled data?
ReCTSi involves multiple components (e.g., MvLC, PCF). How sensitive is the model’s performance to hyperparameter choices? Are there guidelines for practitioners to select optimal configurations?
Ethics Review Flag: No
Ethics Review Description: No issue
Scope: 3: The work is somewhat relevant to the Research track of KDD and is of narrow interest to a sub-community
Novelty: 4: Average
Technical Quality: 3: Below Average
Presentation Quality: 2: Average (it needs some effort to understand, but it should be ok after some editing)
Reproducibility: 3: Excellent (it provides sufficient details, and the code and data are accessible)
Reviewer Confidence: 3: The reviewer is confident but not certain that the evaluation is correct

----------------------------------
Thanks for your time and comments.

$^\S$For detailed visualizations of CaA and experimental results, please refer to [this link](http://bit.ly/49ADwMX).
### Q1 (Non-DL Methods for Small Datasets)：
We would argue that even with a limited number of timestamps, traditional non-DL methods are not necessarily superior to DL methods. This is because real-world time series data, including small datasets, often exhibit complex, nonlinear patterns without clear regularity. Non-DL methods struggle to model such complexity accurately, regardless of dataset size. Conversely, DL methods are adept at capturing intricate correlations within these challenging datasets, demonstrating their ability to effectively model and understand data dynamics, even when faced with limited samples. The experimental results in Table 2 support this observation, illustrating DL methods' superiority in handling rather small datasets.
### Q2 (Scenarios for Non-DL Methods):
We deem that in scenarios with regular, periodic, or stationary data patterns, traditional methods might perform on par with DL-based approaches due to their simplicity and direct applicability to such data characteristics. However, in the context of real-world applications characterized by complex, non-linear patterns and the need to capture intricate spatial and temporal correlations, DL-based methods, including ReCTSi, significantly outshine traditional methods. This advantage is well-documented in contemporary time-series research, where the majority of newly proposed methods leverage deep learning to address the complexities inherent in real-world data effectively.
### Q3/W2 (Generalizability):
Typically, adapting a learning-based model to a specific dataset is a fundamental step in achieving excellent performance. The theoretical guarantee of a model's effectiveness across all datasets, or even specific ones, is challenging. Nonetheless, we provide evidence that the trained ReCTSi performs admirably across diverse domains including traffic flow, air quality, and COVID-19, as shown in Tables 1 and 2 of our original submission.
### Q4 (Visualizations of CaA):
ReCTSi's attention mechanism employs Completeness Matrices to prioritize features' importances based on their completeness, effectively increasing the attention scores for segments with fewer missing values. This approach ensures the model focuses on the most informative parts of the data. To enhance understanding, we've introduced attention-score heatmaps that visually represent the distribution and adjustment of attention weights, highlighting the mechanism's ability to identify and prioritize complete data segments$^\S$.

Regarding the fine-tuned or customized for specific applications, we would argue that ReCTSi is crafted for the general CTS imputation task, demonstrating its effectiveness across various domains such as traffic, air quality, and COVID-19, as well as under different data completeness scenarios. Thus, we think there is no need of additional effort to be fine-tuned or customized for specific applications, only regular hyper-parameter tuning is required for specific applications.
### Q5 (Noisy or Irregularly Sampled Data):
Actually, our work uses real-world datasets, which naturally include noise. The focus of this study is based on the assumption of imputing observed values, hence addressing data noise falls outside our scope. Besides, denoising research often targets specific scenarios with predefined noise characteristics. Thus we suggest users apply targeted denoising techniques suited to their dataset's specific conditions before employing ReCTSi for imputation.

Besides, ReCTSi is engineered to handle both regularly and irregularly sampled datasets. For irregular sampling, adjustments include omitting the PST-pattern codebook tailored for regular intervals. Instead, we utilize the PT-codebook and PS-codebook mechanisms, which assign codes based on timestamp and node index information, irrespective of sampling frequency. Coupled with attention mechanisms that do not depend on temporal sequence, these adaptations ensure ReCTSi seamlessly accommodates irregularly sampled data.

In conclusion, ReCTSi is theoretically capable of handling noisy or irregularly sampled data with minimal modifications, yet exploring this is beyond this paper's scope.
### Q6/W1 (Hyperparameter Study):
Within ReCTSi, there are four main hyperparameters: embedding size, window size, CaA block number, and total codebook size. In the original submission, we have presented the hyperparameter studies of the most important hyperparameters: embedding size and window size in Fig.5. 

Besides, through extensive experiments, we suggest limiting the CaA block number to one or two for optimal performance in the caption of Figure 3. We have added the additional hyper-parameter study$^\S$ of the CaA block number, with one block yielding an MAE of 19.48 on AQ36. Increasing the CaA block number to two or three resulted in higher MAEs of 21.23 and 26.64, respectively. Regarding the total codebook size, our findings indicate a relative insensitivity due to the PCF's compression capabilities. Even with larger codebook sizes, the model maintains stable accuracy (MAE ranging from 19.483 to 20.659 with total codebook size from 24 to 120 on AQ36), as redundant information is efficiently condensed.

Based on these results, we recommend an embedding size comparable to the dataset's channel count for adequate expressiveness and suggest limiting CaA blocks to one or two. A larger initial codebook size is advisable, with PCF ensuring efficient compression. These practical guidelines for configuring ReCTSi will be included in the final version.
### W3 (Balance of Accuracy and Resource Efficiency):
We acknowledge the critical trade-off between accuracy and efficiency. ReCTSi is designed to achieve SOTA performance in both aspects. The experimental results, as detailed in Tables 1 and 2, show that ReCTSi not only consistently achieves SOTA accuracy, ranking top-1 in 14 out of 15 accuracy metrics across five datasets and securing top-2 in all accuracy metrics, but also offers significant resource efficiency. This balance makes ReCTSi particularly compelling for applications where both accuracy and efficiency are critical.
