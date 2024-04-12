We sincerely appreciate your positive assessment of our novelty and quality.

### R1 to Q1, W1, W2 and W3 (Necessity of Edge-resident Imputation and Studies on Diffusions and TST)：
Many edge computing applications necessitates real-time data preprocessing (e.g, data imputation) and decision-making, such as healthcare (e.g, Remote Patient Monitoring) and CPS monitoring (e.g, wind turbine blade icing detection). These applications cannot afford the latency brought by cloud processing, and issues such as network congestion and data privacy further emphasize the need for edge-resident data processing.

Besides, we have added the experimental results of PriSTi (SOTA diffusion-based model) and the ReCTSi-TST variant$^*$. PriSTi and ReCTSi-TST present lower performance metrics, with ReCTSi-TST particularly struggling (e.g., MAE: 36.571 and FLOPs: 0.32M for ReCTSi-TST vs.  MAE: 19.483 and FLOPs: 0.06M for ReCTSI on AQ36), indicating challenges in effectively learning complex TST-patterns through a singular attention module.
### R2 to Q2 (Advanced Attentions for TST):
In fact, we have explored various methods to reduce the complexity of attention modules, including adopting transformer variants during ReCTSi's design. Despite these efforts, we found that these variants led to much imputation accuracy loss (e.g, ReCTSi-Informer adopt the efficient attention mechanism from Informer, presents about 50% FLOPs decrease, while leading to 36% MAE accuracy loss, which is not acceptable)$^*$. Consequently, inspired by Group Converlution, we developed a Grouped FFN mechanism (see Section 4.4), which has been proven to be both effective and efficient. Besides, as mentioned in the previous response, the inferior accuracy of ReCTSi-TST underscored the challenge in effectively learning complex TST-patterns through a singular attention module.
### R3 to Q3, and W4 (Missing Rate Study):
To assess effectiveness and robustness, we conducted a study of the impact of varying missing rates (i.e., 15%, 25%, 35%, and 45%)$^*$. ReCTSi demonstrated remarkable stability and superior performance, maintaining accuracy (e.g., MAE: 18.75-19.96 for PeMs-BA) across all the settings, significantly outperforming the baselines. For instance, PoGeVon, the nearest competitor, recorded higher MAE ranges (e.g., 20.89-22.42 for PeMs-BA).

$^*$For detailed experimental results, please refer to [this link](bit.ly/49ADwMX).

If our response has addressed your concerns, we kindly request that you consider increasing the score.