Thanks for your time and comments.

$^\S$For detailed experimental results, please refer to [this link](http://bit.ly/49ADwMX).

### Q1 (Theoretical Justification):
Our theoretical justification for the decoupled approach and CaA mechanisms is extensively covered in Sections 1 and 4, specifically in Lines 86-94 and 113-129 for the decoupled approach, and Lines 178-199, 515-543, and 545-588 for the CaA mechanism, along with Figures 1 and 4. We explain how these designs enhance ReCTSi by comparing it against end-to-end learning methods. The impact of these designs is further demonstrated through the ablation studies in Tables 4, 6, and 7.
### Q2 (Hyperparameter Study):
Within ReCTSi, there are four main hyperparameters: embedding size, window size, CaA block number, and total codebook size. Actually, we have presented the hyperparameter studies of the most important ones: embedding size and window size in Fig.5. Besides, we suggest limiting the CaA block number to 1 or 2 for optimal performance in the caption of Fig. 3. We have added the study of the CaA block number, with one block yielding an MAE of 19.48 on AQ36$^\S$. Increasing the CaA block number to 2 or 3 resulted in higher MAEs of 21.23 and 26.64, respectively. Regarding the total codebook size, our findings indicate a relative insensitivity due to the PCF's compression capabilities. Even with larger sizes, the model maintains stable accuracy (MAE:19.48-20.66 with the size 24-120 on AQ36), as redundant information is efficiently condensed.
### Q3 (Comparisons with SOTA):
We have indeed conducted comparisons with recent SOTA models, including PoGeVon (KDD'23), and GRIN (ICLR'22), among others. Existing methods employ an end-to-end pattern learning pipeline, and direct comparisons with methods with similar decoupling mechanisms were not available. Furthermore, we did include comparisons with models that incorporate attention mechanisms, such as SAITS.
### Q4 (Limitation):
Following the convention of SOTA works, ReCTSi is evaluated across various domains, including traffic, air quality, and COVID-19, exhibits SOTA accuracy and efficiency. Thus, its underperformance on specific data characteristics cannot be conclusively concluded.
