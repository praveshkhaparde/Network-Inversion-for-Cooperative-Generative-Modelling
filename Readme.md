# **Network Inversion for Cooperative Generative Modelling**
*A cooperative generator–classifier framework that reconstructs training-like samples without directly exposing real data to the generator.*

---

##  Overview

This project implements a **cooperative generative modelling framework** where:

- A **CNN classifier** is trained on the real dataset.  
- A **generator** is trained **simultaneously**, but **never sees the original dataset**.  
- The generator learns purely from the **classifier’s feedback**.  
- Multiple loss functions (Cross-Entropy, KL divergence, Total Variation, Perturbation Entropy, Latent Diversity, SSIM Diversity, etc.) help the generator learn the true data distribution.

This setup demonstrates **network inversion**:  
> reconstructing training-like samples from a classifier by leveraging its internal behaviour, without direct access to the real dataset.

It also provides a stable, interpretable alternative to adversarial GAN-style training.

![1class-no_weights-ce-kld](https://github.com/user-attachments/assets/9cf07e4d-ba2d-4b4f-98d2-05c9e1c9df1c)



---

##  Key Idea


- Classifier learns from real data.  
- Generator never sees real data.  
- Both are trained **from scratch together**.  
- Generator learns class structure through cooperative losses.

---

##  Objectives

- Build a cooperative framework to jointly train a generator and classifier using multiple loss functions.  
- Demonstrate **network inversion** by generating training-like samples without directly using real images in the generator.

---

##  New Ideas Proposed

- Introduced **SSIM-based dissimilarity loss** and **latent diversity loss** to improve semantic variation in generated samples.  
- Reduced total training time by **up to 60%** using:
  - PyTorch profiler for bottleneck removal  
  - Conditional computation of expensive losses  
  - Optimized LR scheduling  
  - Improved data loading  
  - Code-level performance optimizations  

---

##  Training Approach

- Classifier trains on real images using Cross-Entropy.  
- Generator receives:
  - noise vector  
  - one-hot class label  
- Generator updates are guided through:
  - CE on generated labels  
  - KL divergence  
  - Total Variation Loss  
  - Pixel-range Loss  
  - Perturbation Entropy & Perturbed KL  
  - Latent Diversity & SSIM Diversity  
  - Feature Cosine Similarity & Orthogonality (via hooks)

The generator learns the underlying dataset distribution **only through classifier feedback**.

---

##  Challenges Faced

- **Mode collapse**: generator produced nearly identical samples for different noise vectors.  
- **Training instability on larger datasets**: generator gradients interfered with classifier learning, reducing classifier accuracy.  
- High computational cost of multiple loss terms required careful scheduling and conditional execution.

---

##  Who Will Benefit from this Work?

- Researchers studying **network inversion**, **data-free generation**, and **cooperative learning**.  
- ML teams working with **sensitive datasets**, who need synthetic data without exposing real samples to generative models.  
- Practitioners looking for **stable alternatives to GANs**.  
- Privacy & security researchers analyzing **how much information a classifier leaks** when jointly trained with another model.  
- Students exploring generator–classifier interactions and interpretability.

---


