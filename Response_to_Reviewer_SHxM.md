Thank you for the insightful review of our work!
### R1 to Q1 (Scalability):
Thank you for your suggestion! In line with the conventions of recent SOTA methods like PoGeVon and GRIN, we initially utilized the AQ36 dataset for evaluation. Following your suggestion, we extended our experiments to the larger air quality dataset, AQ437, from which AQ36 is derived$^*$. The results affirm ReCTSi's capability to effectively handle datasets with a large sensor count, achieving superior accuracy (MAE: 23.574). Notably, PoGeVon, the second most accurate model on AQ36, encountered the out-of-memory issue on an Nvidia Quadro RTX 8000 GPU and could not be evaluated on AQ437, where other baselines also showed less accuracy (MAE not lower than 29.582).
### R2 to Q2 (Hyperparameter):
Within ReCTSi, there are four main hyperparameters: embedding size, window size, CaA block number, and total codebook size. In the original submission, we have presented the hyperparameter studies of the most important hyperparameters: embedding size and window size in Fig.5. 

Besides, through extensive experiments, we suggest limiting the CaA block number to one or two for optimal performance in the caption of Figure 3. We have added the additional hyper-parameter study of the CaA block number, with one block yielding an MAE of 19.48 on AQ36. Increasing the CaA block number to two or three resulted in higher MAEs of 21.23 and 26.64, respectively. Regarding the total codebook size, our findings indicate a relative insensitivity due to the PCF's compression capabilities. Even with larger codebook sizes, the model maintains stable accuracy (MAE ranging from 19.483 to 20.659 with total codebook size from 24 to 120 on AQ36), as redundant information is efficiently condensed.

Based on these results, we recommend an embedding size comparable to the dataset's channel count for adequate expressiveness and suggest limiting CaA blocks to one or two. A larger initial codebook size is advisable, with PCF ensuring efficient compression. These practical guidelines for configuring ReCTSi will be included in our revision.
### R3 to Q3 (Ability to Capture Long-term Dependencies):
ReCTSi's use of the learnable codebook mechanism in the TPA phase incorporates attention modules specifically chosen for their adeptness at capturing long-term dependencies. Inspired by the efficacy of transformer (i.e., self-attention mechanisms) in managing long-range dependencies within large language models, these modules ensure ReCTSi excels in identifying and leveraging complex temporal relationships over extended periods. This strategic integration of attention-based modules into ReCTSi highlights our commitment to utilizing advanced techniques for profound long-term pattern recognition in time series data.
### R4 to Q4 (Multiple Patterns):
To elucidate the varied patterns within CTS, we use traffic flow as an illustrative example (see Fig. 2 and Lines 144-162). For a better clarification of patterns, we've now organized the information into a clearer format$^*$, accompanied by more detailed explanations.
### R5 to W1 (Overfitting Risks and Dependency on Data Quality):
ReCTSi’s minimal parameter count, significantly lower than baseline models (76K for ReCTSi vs. 191K for the nearest competitor, GRIN), inherently reduces overfitting risks. 

We conducted a comparative analysis across various missing rates (15%, 25%, 35%, and 45%) demonstrates ReCTSi's stable performance and superior accuracy against SOTA models$^*$. Notably, ReCTSi consistently outperformed baselines across all settings, with tighter MAE ranges indicating its robustness to data quality variations (e.g., ReCTSi MAE 18.75-19.96 vs. PoGevon MAE 20.89-22.42, on the PeMs-BA dataset).

$^*$For detailed clarification of patterns and experimental results, please refer to [this link](bit.ly/49ADwMX).

If our response has addressed your concerns, we kindly request that you consider increasing the score.
