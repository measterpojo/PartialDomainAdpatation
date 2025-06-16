# PartialDomainAdpatation
Partial Domain Adaptation (PDA) is a domain adaptation scenario where the target domain's label space is a subset of the source domain's label space


Class Conditional Alignment (CCA-PDA)

CCA - is a well-designed method for partial domain adaptation that directly tackles the class mismatch issue between source and target domains.

It uses a multi-class adversarial loss to perform this alignment, ensuring that only the shared classes between source and target are emphasized. This helps avoid negative transfer from source-only classes.


Datasets

Caltech as the source and Office-31 as the target is a classic partial domain adaptation (PDA) scenario, since Caltech has a broader label space (256 classes) while Office-31 has only 31. This means you’ll need to filter out the irrelevant Caltech classes to avoid negative transfer.

upload caltech source from kaggle


Trained discriminator for class 0 | src: 30607, tgt: 1106, loss: 0.6472
Trained discriminator for class 1 | src: 30607, tgt: 1711, loss: 0.6960
Skipping class 2: not enough samples (src: 0, tgt: 0)
Skipping class 3: not enough samples (src: 0, tgt: 0)
Skipping class 4: not enough samples (src: 0, tgt: 0)
Skipping class 5: not enough samples (src: 0, tgt: 0)
Skipping class 6: not enough samples (src: 0, tgt: 0)
Skipping class 7: not enough samples (src: 0, tgt: 0)
Skipping class 8: not enough samples (src: 0, tgt: 0)
Skipping class 9: not enough samples (src: 0, tgt: 0)


Possible Causes:

Classifier bias toward a few classes

Your classifier might be overfitting to dominant classes in Caltech-10, ignoring others when assigning pseudo-labels.

Some classes may have lower feature separability, making the softmax outputs less confident.

Target domain shift

Domain shift causes category mismatch—even if some objects in Office-31 belong to a "shared" class, the visual domain is different enough that your classifier might not recognize them confidently.

Confidence threshold cutting too aggressively

If your threshold (confidence_threshold = 0.7) is too high, most target samples won’t qualify as confidently pseudo-labeled.

Lowering it to 0.5 or even 0.3 might help populate more classes.
