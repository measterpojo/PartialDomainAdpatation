# PartialDomainAdpatation
Partial Domain Adaptation (PDA) is a domain adaptation scenario where the target domain's label space is a subset of the source domain's label space


Class Conditional Alignment (CCA-PDA)

CCA - is a well-designed method for partial domain adaptation that directly tackles the class mismatch issue between source and target domains.

It uses a multi-class adversarial loss to perform this alignment, ensuring that only the shared classes between source and target are emphasized. This helps avoid negative transfer from source-only classes.


Datasets

Caltech as the source and Office-31 as the target is a classic partial domain adaptation (PDA) scenario, since Caltech has a broader label space (256 classes) while Office-31 has only 31. This means you’ll need to filter out the irrelevant Caltech classes to avoid negative transfer.

upload caltech source from kaggle


### Class-Wise Discriminator Training Results
During the **Class Conditional Alignment (CCA-PDA) process**, discriminators are trained per class to distinguish source vs. target domain features. The results below indicate which classes successfully received target samples and which were skipped due to insufficient data.

#### Training Summary
| Class Index | Source Samples | Target Samples | Status  | Loss Value |
|------------|---------------|---------------|--------|------------|
| 0          | 30,607        | 1,106         | ✅ Trained | 0.6472 |
| 1          | 30,607        | 1,711         | ✅ Trained | 0.6960 |
| 2          | 0             | 0             | ⚠️ Skipped | N/A |
| 3          | 0             | 0             | ⚠️ Skipped | N/A |
| 4          | 0             | 0             | ⚠️ Skipped | N/A |
| 5          | 0             | 0             | ⚠️ Skipped | N/A |
| 6          | 0             | 0             | ⚠️ Skipped | N/A |
| 7          | 0             | 0             | ⚠️ Skipped | N/A |
| 8          | 0             | 0             | ⚠️ Skipped | N/A |
| 9          | 0             | 0             | ⚠️ Skipped | N/A |

### Key Observations
- **Classes 0 & 1 trained successfully**, meaning the model was able to extract enough target samples to align them.
- **Classes 2–9 were skipped** due to zero source or target samples, implying either dataset mismatch, category absence, or confidence filtering.
- Lowering the **confidence threshold** (currently `0.7`) may increase target samples for more classes.

### Next Steps
1. **Verify class overlap** between the source (Caltech-10) and target (Office-31) domains.
2. **Visualize target feature distributions** to confirm if missing classes exist but lack high-confidence predictions.
3. **Adjust pseudo-labeling strategies** to better populate underrepresented classes.



Possible Causes:

Classifier bias toward a few classes

Your classifier might be overfitting to dominant classes in Caltech-10, ignoring others when assigning pseudo-labels.

Some classes may have lower feature separability, making the softmax outputs less confident.

Target domain shift

Domain shift causes category mismatch—even if some objects in Office-31 belong to a "shared" class, the visual domain is different enough that your classifier might not recognize them confidently.

Confidence threshold cutting too aggressively

If your threshold (confidence_threshold = 0.7) is too high, most target samples won’t qualify as confidently pseudo-labeled.

Lowering it to 0.5 or even 0.3 might help populate more classes.
