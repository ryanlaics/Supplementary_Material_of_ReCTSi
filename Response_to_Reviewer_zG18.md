Review:

Quality:

While the overall quality of "ReCTSi" is commendable for its innovation in time series imputation, there are areas where rigor could be improved. The methodology, though innovative, requires a more rigorous statistical validation. The assumptions underlying the decoupled pattern learning and the completeness-aware mechanisms should be critically examined against diverse datasets with varying levels of sparsity and noise. Additionally, the quality of the experimental evaluation could be enhanced by including more challenging baselines or state-of-the-art methods that employ similar or competing strategies.

Clarity:

The manuscript, while generally clear, occasionally delves into complex descriptions without adequate simplification or clarification, which could alienate readers not deeply versed in time series imputation or deep learning. Key concepts and algorithmic steps, particularly around the decoupled learning process and completeness-aware attention, need clearer exposition and possibly visual aids to improve accessibility and understanding. The clarity of presentation regarding the mathematical foundation and empirical evidence could be enhanced.

Originality:

The originality of the proposed ReCTSi framework is notable; however, the work could be better positioned within the current landscape of time series imputation research. A more comprehensive review of the existing literature, including the latest advancements and how they compare to ReCTSi in terms of not only performance but also computational efficiency, would better highlight the novelty of the proposed approach. Additionally, the unique contributions of ReCTSi beyond combining existing concepts like decoupling learning phases and attention mechanisms should be more explicitly articulated.

Significance:

The significance of the proposed work to the field and real-world applications is evident but not fully exploited. The implications of ReCTSi for practical applications, particularly in scenarios with severe resource constraints or in different domains, need a deeper discussion. Furthermore, while the paper claims significant improvements in computational efficiency, the practical impact of these improvements (e.g., on battery life in mobile applications, real-time processing capabilities) is not adequately explored.

Pros:

Innovative Combination of Techniques: The integration of decoupled pattern learning with completeness-aware attention is a commendable attempt at addressing CTS imputation.

Resource Efficiency Emphasis: Focusing on reducing computational resources is timely and relevant, particularly for edge computing and IoT applications.

Cons:

Lack of Theoretical Justification: The paper lacks a solid theoretical framework justifying why the decoupled approach and completeness-aware attention should lead to better performance or efficiency.

Insufficient Comparison: The experimental comparisons seem limited, lacking in diversity of datasets and failure to compare with the latest or most directly relevant methods.

Hyperparameter Exploration: There is minimal discussion on how hyperparameters were chosen and their sensitivity, which is crucial for reproducibility and practical application.

Real-world Applicability: Discussions on real-world applicability are superficial and need concrete examples or case studies to demonstrate ReCTSi’s practical benefits.

Limitations and Challenges: The manuscript does not sufficiently address potential limitations, challenges, or scenarios where ReCTSi may not perform well.

In conclusion, "ReCTSi" presents a promising approach to CTS imputation with a focus on resource efficiency. However, for the work to truly stand out, it requires deeper theoretical grounding, broader and more rigorous experimental validation, clearer articulation of its originality and significance, and a more thorough exploration of its practical applicability and limitations.

Questions:
Theoretical Justification: Can you provide a more detailed theoretical justification or intuition behind the decoupled pattern learning approach and completeness-aware attention mechanisms? How do these methodologies specifically contribute to improving imputation accuracy and computational efficiency?

Hyperparameter Sensitivity and Selection: Could you elaborate on the selection process for your model’s hyperparameters? How sensitive is ReCTSi's performance to these hyperparameters, and did you perform a systematic analysis or validation to determine their optimal values?

Comparative Analysis with Recent Methods: Your experimental comparisons include several baseline methods, but could you discuss how ReCTSi compares to the most recent state-of-the-art methods in time series imputation, particularly those that might use similar decoupling or attention mechanisms?

Limitations and Failure Cases: Every method has its limitations. Can you discuss specific scenarios or data characteristics where ReCTSi might underperform? How does the method cope with extremely sparse datasets or datasets with non-random missingness patterns?

Ethics Review Flag: No
Ethics Review Description: No ethics concerns
Scope: 3: The work is somewhat relevant to the Research track of KDD and is of narrow interest to a sub-community
Novelty: 4: Average
Technical Quality: 3: Below Average
Presentation Quality: 2: Average (it needs some effort to understand, but it should be ok after some editing)
Reproducibility: 2: Average (some information is missing, but that could be easily fixed in the camera-ready version)
Reviewer Confidence: 3: The reviewer is confident but not certain that the evaluation is correct

----------------------------------
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
