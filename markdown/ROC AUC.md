The Reciever Operator Characterstics (ROC) is plot between TPR and FPR at different classification thresholds.

The TPR (same as recall or sensitivity) is defined as follows

$$
TPR = \frac{TP}{TP+FN}
$$
Similarly FPR is defined as follows
$$
FPR = \frac{FP}{FP+TN}
$$
which is equal to 1-Recall ($TNR$)of negative class (Specificity)

$TP+FN$ = Total num of positive labels in ground truth
$FP+TN$ = Total num of negative labels in ground truth.

As classification threshold increases, both TPR and FPR decreases because as classification threshold increases $FNs$ will increase and $TP$ will decrease which leads to low TPR. Similary $FPs$ will decrease and $TNs$ will increase leading to decrease in $FPR$. 

The area under the curve for a random classifier is 0.5 and a perfect classifier at all classification thresholds will have area under the curve 1. So a better model will have ROC AUC score between $0.5<score<1.0$.

## Notes

1. It is a single metric independent of thresholds
2. Doesn’t takes in to account the fact that sometimes FP or FN can be more costly. In this case it is better to use recall or precision as metric.
3. Can be used to compare models.


## Probabilistic Interpretation

