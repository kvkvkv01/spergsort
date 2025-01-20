# SpergSort

SpergSort is a sophisticated sorting tool that uses statistical methods to rank items based on pairwise comparisons. Unlike traditional sorting algorithms, it handles subjective preferences and noisy comparisons gracefully by implementing the Bradley-Terry model with adaptive pair selection.

## Features

- **Statistical Sorting**: Uses Bradley-Terry model for robust preference ranking
- **Adaptive Selection**: Intelligently chooses pairs to minimize required comparisons
- **Confidence Metrics**: Shows real-time confidence levels and sorting progress
- **Dynamic Scaling**: Adjusts requirements based on set size
- **Result Analysis**: Generates statistics and visualizations of preferences
- **Seed System**: Save and share your progress with seeds
- **Export**: Generate images of final rankings with statistics

## Usage

1. **Start New Sort**:
   - Choose a filter if needed
   - Click \"Start New Sort\"
   - Compare pairs by clicking on preferred items

2. **Continue from Seed**:
   - Paste your seed in the input field
   - Click \"Load Seed\"
   - Continue where you left off

3. **Generate Results**:
   - Wait for fair confidence level
   - Click \"Generate Rankings Image\"
   - Or copy seed to share your progress

## Technical Details

### Pair Selection Algorithm

SpergSort uses a weighted scoring system for pair selection:
```javascript
score = comparisons_count - (uncertainty / 1000) + time_penalty
```

- Fewer comparisons → higher priority
- Higher uncertainty → higher priority
- Recent comparison → lower priority

### Confidence Calculation

For n items:
- Target comparisons = n * log2(n) * 0.3
- Target uncertainty = 100 * sqrt(n/10)

Confidence increases with:
- More comparisons per member
- Clear preference distinction
- Consistent choices

## Credits

- Mathematical foundation based on [Gwern's research on resorting](https://gwern.net/sorting)
- Inspired by Bradley-Terry model for paired comparisons
- Created by [kanon](https://x.com/oonomoco)

---
© 2024 Little Japanese Girl Technologies
