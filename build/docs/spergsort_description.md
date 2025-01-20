# 乃木坂46 SpergSort: Statistical Adaptive Sorting

SpergSort is an implementation of adaptive sorting using the Bradley-Terry model for paired comparisons. Based on Gwern's research on [noisy sorting](https://gwern.net/sorting), it provides a statistically robust way to rank items through pairwise comparisons.

## Mathematical Foundation

### Bradley-Terry Model

At its core, SpergSort uses the Bradley-Terry model which posits that each item i has a latent "strength" parameter $\beta_i$, and the probability of item i being preferred over item j is:

$$P(i \text{ beats } j) = \frac{\exp(\beta_i)}{\exp(\beta_i) + \exp(\beta_j)}$$

### Adaptive Selection

Rather than using a fixed comparison sort algorithm, SpergSort employs an adaptive strategy that prioritizes comparisons that would be most informative. For each potential comparison between items i and j, we calculate a score:

$$\text{score}_{ij} = c_{ij} - \frac{|\beta_i - \beta_j|}{1000} + p_{ij}(t)$$

Where:
- $c_{ij}$ is the number of previous comparisons between i and j
- $|\beta_i - \beta_j|$ represents uncertainty (larger differences suggest more certain ordering)
- $p_{ij}(t)$ is a time penalty that decreases as time passes since the last comparison

### Confidence Level

The confidence in our sorting is determined by two factors:
1. Average comparisons per item ($\bar{c}$)
2. Standard deviation of scores ($\sigma$)

For n items, we target:
$$\bar{c} = \lceil n \log_2(n) \cdot 0.3 \rceil \text{ comparisons}$$
$$\sigma_{target} = 100\sqrt{\frac{n}{10}} \text{ score spread}$$

## ELI5: Sorting with Fruits 🍎🍌🍊

Imagine you have a basket of different fruits and you want to rank them by how much you like them. But here's the catch - you can only compare two fruits at a time!

### How It Works (Simple Version)
1. The app shows you two fruits
2. You pick which one you like better
3. The app remembers your choice
4. It keeps showing you different pairs
5. Eventually, it figures out your complete ranking!

For example:
- Round 1: 🍎 vs 🍌 (you pick 🍎)
- Round 2: 🍊 vs 🍎 (you pick 🍊)
- Round 3: 🍊 vs 🍌 (you pick 🍊)

Final ranking: 
1. 🍊 Orange (best)
2. 🍎 Apple (second)
3. 🍌 Banana (third)

### Why It's Smart
- If you change your mind, it adapts!
- It remembers how sure you are about each choice
- It tries to ask you the most helpful questions

Think of it like a really smart game of "which do you prefer?" that learns from your answers!

## Technical Details

The implementation uses:
- Weighted random selection for pair choosing
- Time-based penalties to avoid repetitive comparisons
- Dynamic confidence thresholds based on set size
- Adaptive exploration vs exploitation balancing

References:
- Gwern (2019). ["Noisy Sorting"](https://gwern.net/sorting)
- Bradley & Terry (1952). "Rank Analysis of Incomplete Block Designs"
- Davidson (1970). "On extending the Bradley-Terry model"