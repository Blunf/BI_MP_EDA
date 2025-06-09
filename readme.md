## P1

## P2 

### HybridSVD Model (vs. Original SVD)

https://paperswithcode.com/paper/hybridsvd-when-collaborative-information-is

#### 1. Introduction

**SVD** is a well-known SVD-based collaborative filtering method. While it offers speed and simplicity, it suffers from critical limitations—especially when user-item interactions are sparse or when new users/items appear (cold start problem).  
**HybridSVD** addresses these limitations by incorporating side information (e.g., user attributes or item features) into the SVD framework without sacrificing computational efficiency.

#### 2. Key Differences

| Aspect                     | PureSVD                                      | HybridSVD                                                      |
|---------------------------|----------------------------------------------|----------------------------------------------------------------|
| Uses side information     | ❌ No                                         | ✅ Yes                                                         |
| Cold start support        | ❌ Weak                                       | ✅ Strong (through feature mapping)                            |
| Flexibility of latent space | ❌ Fixed (cosine-based latent space)         | ✅ Adaptive (informed by user/item similarity)                 |
| Complexity                | ✅ Simple and efficient                       | ✅ Slightly more complex, but optimized via Cholesky methods   |
| Folding-in (online update) | ✅ Supported                                  | ✅ Supported, with enhanced latent space                        |
| Parameter tuning          | ✅ Easy (rank truncation)                     | ✅ Easy (same with additional α, β parameters)                 |


#### 3. Advantages of HybridSVD

**Incorporates Side Information**

By modeling auxiliary similarities between users and items, HybridSVD can utilize genres, brands, demographic attributes, etc.

**Solves the Cold Start Problem**

HybridSVD learns mappings from features to latent vectors, allowing recommendation even when no interaction history exists.

**Retains PureSVD Strengths**

It keeps fast convergence, rank truncation, folding-in, and compatibility with sparse data.


#### 4. When to Use HybridSVD

- The dataset is sparse (e.g., e-commerce with many items but few purchases)
- Cold start items or users are common
- Side information is rich and reliable
- Real-time recommendation is required