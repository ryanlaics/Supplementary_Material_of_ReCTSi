We sincerely thank you so much for the positive evaluation of our work's novelty and quality!
### R1 to Q1 （Confusion of the Same Notation t）:
Thank you for highlighting this issue. We will clarify the notation of t in Eq. (4), (6) in the revised manuscript to prevent any confusion.
### R2 to Q2（Assumption of CaA）:
In CaA, the self-attention mechanism can address the long-term dependancy issue, where the features from neither neighbour or distant segments can be processed equally in CaA. However, the vanilla self-attention mechanism cannot consider the data reliability (which is indicated by the completeness of data segment). ReCTSi’s CaA employs a nuanced approach to address this: it leverages the self-attention mechanism to evaluate both nearby and distant data segments without bias, focusing on their informational completeness rather than just proximity. This is crucial because, in cases where a neighboring segment is largely missing, its contribution to understanding the current data point is minimal, rendering it less reliable. Conversely, a distant segment with complete data can offer valuable insights, deserving a higher weight in the analysis. Thus, ReCTSi’s strategy of prioritizing data reliability and completeness allows for more accurate pattern extraction.
### R3 to Q3 (Rationale of Using Grouped FFN):
In fact, we have explored various methods to reduce the complexity in the TPA's attention modules, including adopting advanced transformer variants during ReCTSi's design. Despite these efforts, we found that existing alternatives led to accuracy losses for the imputation task$^*$ (e.g, ReCTSi-Informer variant adopt the efficient attention mechanism from Informer, presents about 50% FLOPs decrease, while leading to 36% accuracy loss, which is not acceptable). Consequently, motivated by Group Convolution, we then formulated the Grouped FFN mechanism. The adoption of GFN balances efficiency with effectiveness, avoiding the accuracy compromises observed in previous iterations. 

$^*$For detailed experimental results, please refer to [this link](bit.ly/49ADwMX).

If our response has addressed your concerns, please consider increasing the score.
