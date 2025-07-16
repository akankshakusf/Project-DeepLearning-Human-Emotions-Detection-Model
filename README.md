# Project-DeepLearning-Human-Emotions-Detection-Model-

 Introduction
Welcome! This repository is a comprehensive, research-driven exploration of deep learning methods for emotion recognition from facial images. My work benchmarks several state-of-the-art (SOTA) architectures—ranging from foundational CNNs (ResNet, VGG) to modern transformer-based models (ViT, Hugging Face’s ViT)—on a real-world, imbalanced dataset with three core classes: happy, sad, and angry.

Throughout this project, I emphasize:

Systematic experimentation

Interpretability (feature maps, GradCAM, patch visualizations)

Model robustness (handling class imbalance, cross-architecture ensembling)

Transparent reporting—with metrics, confusion matrices, and qualitative outputs.

📦 Project Pipeline
1. Data Preprocessing & Augmentation

Images are standardized, resized, and augmented (rotation, brightness, flipping).

Special care is taken to address class imbalance (see below).

2. Baseline: ResNet-34

Trained from scratch on the dataset.

Used as a performance anchor.

Best Val Accuracy: ~52%

Findings: Standard CNNs struggle to capture nuanced expressions, especially with limited data.

3. Transfer Learning: EfficientNetB4

Loaded ImageNet weights; experimented with both frozen and unfrozen backbone.

Class weighting applied to loss function to combat data imbalance (angry/sad less represented).

Best Val Accuracy: ~76%

Findings: Transfer learning provides a significant boost; EfficientNet learns compact, rich representations, especially when fine-tuned.

4. Feature Map Analysis: VGG-16

Used for in-depth interpretability (visualizing intermediate convolutional activations).

Provided insights into where in the image (eyes, mouth, wrinkles) different emotions are detected.

5. Custom Vision Transformer (ViT)

Implemented from scratch: patching, positional embeddings, transformer encoder layers, and MLP heads.

Findings: Custom ViT struggled with limited data, plateaued at ~44% accuracy, illustrating the data hunger and pretraining needs of ViTs.

6. Model Ensembling

Combined ResNet-34 and EfficientNet outputs with soft averaging.

Modest improvements in stability and recall on minority classes.

7. Hugging Face ViT (google/vit-base-patch16-224-in21k) — SOTA

Loaded pre-trained ViT from Hugging Face.

Integrated with Keras for end-to-end fine-tuning.

Leveraged class weighting, robust data augmentation, and advanced experiment tracking (wandb).

Achieved SOTA:

Val/Test Accuracy: ~96.9%

Confusion Matrix: Minimal off-diagonal confusion—model generalizes very well.

Interpretability: Visualized patch-level attention and saliency.

🏅 Benchmark Results
Model	Approach	Best Val Accuracy	Key Insights
ResNet-34	Baseline CNN	~52%	Misses subtle emotions
EfficientNetB4	Transfer Learning	~76%	Handles imbalance, robust
Vision Transformer	Custom Implementation	~44%	Needs more data/pretrain
Ensemble	ResNet+EffNet Averaged	~84%	Boosts recall, stability
Hugging Face ViT	Pre-trained ViT (SOTA)	96.9%	Best across all metrics

Key Metric Examples (Hugging Face ViT):

Accuracy: 0.969 (Val/Test)

Loss: ~0.11

Top-2 Accuracy: 1.00

Confusion Matrix:

Sample Predictions:

🔬 Deep Dives
Model Interpretability
VGG-16 Feature Maps:
Analyzed early, mid, and late-layer activations. Early layers focus on edges and textures; deeper layers on facial regions and shapes—mouths for “happy,” eyes/eyebrows for “sad” and “angry.”

ViT Patch Visualizations:
Custom code to split faces into 16x16 patches, reconstructed images from patches to understand which facial regions contribute most to final predictions.

WandB Integration:
All training runs, predictions, and confusion matrices tracked live and shared for full transparency.

Class Imbalance Strategy
Dynamic Class Weights:
Computed per epoch (e.g., {happy: 2.25, sad: 3.01, angry: 4.45}) and applied during training.

Result: Boosted recall for underrepresented classes, improving overall F1 and reducing systematic bias.

Practical Takeaways
SOTA pre-trained transformers dominate on facial emotion recognition—even with moderate dataset sizes.

Interpretability techniques build trust—essential for real-world adoption (health, security, HR).

Class weighting and augmentation are must-haves for applied computer vision projects with imbalanced or noisy data.

💡 Why This Project?
Real-World Impact: Emotion detection powers digital well-being, healthcare, human-computer interaction, and content moderation.

End-to-End Mastery: I show all steps: from classical deep learning to transformers, rigorous benchmarking, explainability, and production-ready deployment.

Research & Engineering Blend: Custom code, in-depth experiments, and results communicated like a true data scientist.
