# wafer-categoriser

## Data received from the manufacturing process
The data sent over consisted of 14,236 images. These were classified as different categories as summarised in the table below:

| index | Label | Count | Percentage |
| ---- | ---- | ---- | ---- |
| 0 | none | 13489 | 93\.8953 |
| 1 | Loc | 297 | 2\.0674 |
| 2 | Edge-Loc | 296 | 2\.0604 |
| 3 | Center | 90 | 0\.6265 |
| 4 | Random | 74 | 0\.5151 |
| 5 | Scratch | 72 | 0\.5012 |
| 6 | Edge-Ring | 31 | 0\.2158 |
| 7 | Near-full | 16 | 0\.1114 |
| 8 | Donut | 1 | 0\.007 |

## Automation
We think it is possible to automate all of this task. The automation can be done in phases. We observed that there is a high number of uncategorised discs. Thus, an initial model that identifies wafers that are categorised and uncategorised is the first step. This could result in a ~93% reduction in the time taken to review and classify as a major chunk of the wafers need not be classified.

## Methodology
- We adopted a two-step modelling approach. The initial model focuses on discerning and predicting the distinction between categorised and uncategorised wafers. Subsequently, the second model is employed to predict specific categories.
- To maintain a balanced representation of each class in the test results comparable to the training and overall test sets, we implemented a stratified split during the creation of the test dataset.
- The test set is derived from 20% of the complete dataset, ensuring a proportionate inclusion of each class in the evaluation process
- To compensate for the the huge class imbalance, categories that were underrepresented were adjusted by using oversampling.

## Results
- Total accuracy: 99.6%
- Recall: Most classes have a high value of recall
- Precision: This metric represents how many of the predicted values were actually true. The precision is in general high, with most values more than 99%
- “Support” labelled in the table is the number of test cases for each class
- Accuracy of Categorisable wafers that were predicted as not-categorisable: 14 - Ideally this number should be very low, nearly zero.

## Potential methods to improve accuracy of automation

There are 2 phases to how we can achieve better results:

1. **Improve precision for identifying uncategorised Vs categorised wafers (the 99% in current results):**
   - **Precision-centric Training:** Enhance the model's precision by prioritizing it as a training metric. Focusing on precision ensures a lower rate of false positives.
   - **Adjusting Confidence Threshold:** Increase the model's confidence by utilizing a higher threshold during predictions. This helps in making more conservative predictions, reducing false positives. In our scenario, we need to be more conservative about ensuring low False Negatives for the “None” class.

2. **Improve categorization of different categories:**
   - The current data is lacking in samples of different categories. This can be fixed in the following ways:
      2.1 **Augment existing images:** Address the scarcity of samples for different categories by augmenting existing images. Techniques involve:
         - Rotating the images by 90 degrees,
         - Padding the images and then rotating them by different angles,
         - Reflecting the images to create diverse samples.
      2.2 **Collecting additional data:** Continuously improve model training by gathering more data over time. As the dataset expands, the model gains exposure to a wider variety of samples, contributing to improved categorization accuracy.

