[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/5HZkrI_Y)
[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/r8OAyKH-)
# CNN Classification — Cat vs. Dog

## Dataset
**Cats vs Dogs** — [Kaggle](https://www.kaggle.com/datasets/shaunthesheep/microsoft-catsvsdogs-dataset)  
~25,000 JPEG images 

## Preprocessing
- Resized all images to `128×128`
- Normalized pixel 
- Split: **70% Train / 15% Val / 15% Test**

## Models

### Model 1 — 3 Conv Layers
| Layer | Details |
|---|---|
| Conv2D × 3 | 32 → 64 → 128 filters, ReLU |
| MaxPooling2D × 3 | 2×2 |
| Dense | 256 neurons, ReLU |
| Dropout | 0.5 |
| Output | 1 neuron, Sigmoid |

### Model 2 — 4 Conv Layers
Same as Model 1 + extra `Conv2D(256) + MaxPooling2D` block.

**Compile:** Adam | Binary Crossentropy | Accuracy  
**Training:** 10 epochs, Batch size 64, EarlyStopping (patience=5)

## Results

| Metric | Model 1 | Model 2 |
|---|---|---|
| Accuracy | 0.8368 | **0.8814** |
| Precision | 0.8264 | **0.8944** |
| Recall | 0.8553 | **0.8665** |
| F1-Score | 0.8406 | **0.8802** |

## Findings
- **Model 2 outperforms Model 1** across all metrics, with ~4.5% accuracy gain from adding a 4th Conv layer.
- Both models show **overfitting** in later epochs  Train Accuracy kept rising while Val Accuracy stopped improving.
- Model 1 correctly classified all 7 real-world test images, while Model 2 misclassified 2 out of 7, suggesting Model 1 generalizes better despite lower test set accuracy.
- Adam's default learning rate (0.001) provided stable convergence for both models.