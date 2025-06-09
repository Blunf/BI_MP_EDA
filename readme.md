## P1 - TextSentiment


## P2 - HybridSVD Model (vs. Original SVD)

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



## P4 - ICF - RCF

.

.



###  Item Collaborative Filtering

Suppose user **A** has watched the movies "E.T." and "Indiana Jones."

- Traditional item-based collaborative filtering (ICF) recommends movies to **A** based on what other users with similar viewing histories have also watched.
- In other words, recommendations are based solely on *co-viewing patterns*:
  > "People who watched these movies also watched..."


### But RCF ->  Leveraging Multiple Item Relations

**RCF (Relational Collaborative Filtering)** is a recommender system framework that leverages multiple item relations, going beyond the traditional collaborative filtering approach. Below, you'll find a clear markdown explanation with real-world examples.

RCF doesn't just look at co-viewing. It considers various explicit relationships between items (movies, songs, etc.), such as:

- **Same director:** "E.T." and "Schindler's List" are both directed by Steven Spielberg.
- **Same genre:** "E.T." and "The Avengers" are both science fiction.
- **Same actor:** "E.T." and another movie might share an actor.


.

.

.


#### Movie Recommendation Example



##### Scenario

User **B** has watched "E.T."  
There are several possible relations between "E.T." and other movies:

- **Director:** "E.T." and "Schindler's List" (both by Spielberg)
- **Genre:** "E.T." and "The Avengers" (both science fiction)
- **Actor:** "E.T." and another movie with the same actor

##### How RCF Recommends

1. **Classify by relation type:** Identify all possible relations (director, genre, actor, etc.) between "E.T." and candidate movies.
2. **First-level attention:** Determine which relation types matter most to user **B**.
   - For example, if **B** cares more about genre, movies with the same genre as "E.T." get higher weight.
3. **Second-level attention:** Within each relation type, assess which specific values (e.g., "science fiction" vs. "action") or which directors/actors are most relevant to **B**.
   - If **B** especially likes science fiction, those movies are prioritized.
4. **Final recommendation:** Combine **B**'s interaction history and their relation-based preferences to recommend, for example, "The Avengers" (same genre) or "Schindler's List" (same director).

##### Example Recommendation Explanations

- Recommending "The Avengers":
  > "Recommended because both 'E.T.' and 'The Avengers' are science fiction movies you like."
- Recommending "Schindler's List":
  > "Recommended because you like movies directed by Steven Spielberg."

RCF thus provides both personalized recommendations and clear explanations based on diverse item relations.

### Summary Table: ICF vs. RCF

| Aspect                | Traditional ICF                              | RCF (Relational Collaborative Filtering)                |
|-----------------------|----------------------------------------------|--------------------------------------------------------|
| Main signal           | Co-viewed/co-purchased items                 | Multiple explicit item relations (director, genre, etc.)|
| Personalization       | Based on similar users or items              | Based on user-specific relation preferences            |
| Explanation           | Limited ("People also watched...")           | Rich ("Same director/genre as movies you liked")       |
| Example               | "People who watched X also watched Y"        | "Recommended because both are sci-fi movies"           |

