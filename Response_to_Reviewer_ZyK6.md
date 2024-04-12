Review:
This paper proposes a framework that adopts architecture decoupling and learnable codebook techniques for resource-efficient time-series imputation. The experimental results indicate a significant improvement in imputation accuracy while enjoying lower latency and model complexity.

Strengths

(+) The paper tackles important problems in real-world time-series data often having missing values.
(+) The paper provides a strong experiment result substantiating the claims.
(+) Each design choice (PPE & TPA+CaA) included in the framework is well-justified.
Weaknesses

(-) In general, the imputation task is considered as a preprocessing step in the entire pipeline. I am not sure about the necessity of making the imputation in resource-limited edge settings.
(-) The paper mentions that TST patterns incur quadratic space and time complexity. However, it should be included if it can provide more imputation accuracy, considering the current runtime latency.
(-) Lack of comparison with the recent diffusion models.
(-) I am not sure how the imputation accuracy of the models changes with respect to the different missing rates.
Questions:
Q1. As mentioned above, because the imputation is usually run before downstream training and deployment, I am not certain that latency should be a big concern in this context. Therefore, comparing more recent diffusion models and incorporating the TST patterns should make the paper more solid.

Q2. In addition, the paper argues the complexity of the TST patterns based on only the vanilla attention mechanism. However, there are many recent efficient attention mechanisms [a] for time series that can also be used in this framework.

Q3. It would be better if the paper shows the experiment results comparing the imputation accuracy across different missing rates.

[a] Wen, Qingsong, et al. "Transformers in time series: a survey." Proceedings of the Thirty-Second International Joint Conference on Artificial Intelligence. 2023.

Ethics Review Flag: No
Ethics Review Description: N/A
Scope: 3: The work is somewhat relevant to the Research track of KDD and is of narrow interest to a sub-community
Novelty: 5: Above Average
Technical Quality: 5: Above Average
Presentation Quality: 3: Excellent (it is a pleasure to read and easy to understand, it has good figures and insightful explanations)
Reproducibility: 3: Excellent (it provides sufficient details, and the code and data are accessible)
Reviewer Confidence: 3: The reviewer is confident but not certain that the evaluation is correct

----------------------------------
Thanks for your time and comments.

$^\S$For detailed experimental results, please refer to [this link](http://bit.ly/49ADwMX).

### Q1/W1/W2/W3 (Necessity of Edge Imputation & Studies on Diffusion and TST)：
Indeed, various applications such as Remote Patient Monitoring and Wind Turbine Blade Icing Detection, desire fast data preprocessing (like imputation) and decision-making at the edge. They cannot afford the latency brought by cloud processing, and issues like network congestion and data privacy further emphasize the need for edge-resident data processing.

Besides, we added experimental results for PriSTi (diffusion-based SOTA), and ReCTSi-TST variant$^\S$. PriSTi achieves better accuracy (MAE: 17.384) but at the cost of significantly lower efficiency, with 6517× FLOPs, 10× peak memory and parameter counts, and 6561× latency compared to ReCTSi. This inefficiency makes them unsuitable for edge scenarios, which is why we exclude diffusion models in the submission. Besides, ReCTSi-TST underperforms (MAE: 36.571 and FLOPs: 0.32M) relative to ReCTSi (MAE: 19.483 and FLOPs: 0.06M), indicating challenges in learning complex TST-patterns through a single module. These insights will be further discussed in the final version.

## Q2 (Advanced Attentions):
Yes, we have explored various methods to reduce the complexity of attention modules, including adopting transformer variants during ReCTSi's design. Despite these efforts, these variants led to much accuracy loss (e.g., ReCTSi-Informer adopt the attention mechanism from Informer, presents about 50% FLOPs decrease, while leading to 36% MAE accuracy loss, which is not acceptable)$^\S$. Instead, inspired by Group Conv, we developed a Grouped FFN mechanism (see Section 4.4) to reduce the computational overheads of vanilla FFN. Besides, as mentioned in the above response, the inferior accuracy of ReCTSi-TST underscored the challenge in effectively learning complex TST-patterns via a singular attention module.

### Q3/W4 (Missing Rate Study):
To assess effectiveness and robustness, we conducted a study of the impact of varying missing rates (15%-45%)$^\S$. ReCTSi demonstrated remarkable stability and superior performance, maintaining accuracy (e.g., MAE: 18.75-19.96 for PeMs-BA) across all the settings, significantly outperforming the baselines. For instance, PoGeVon, the nearest competitor, recorded much higher MAE ranges (20.89-22.42 for PeMs-BA).
