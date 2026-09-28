# Chart Selection Guide

Choose the chart from the question and data structure, not from appearance.

## 1. Correlation / relationship

Use when the question is how variables move together or whether groups occupy different regions.

- **Scatter**: default for two numeric variables.
- **Transparent scatter / hexbin / binned density**: large or overplotted datasets.
- **Regression scatter**: relationship plus fitted trend; do not imply causality.
- **Marginal distributions**: scatter plus histograms/KDE when joint and individual distributions both matter.
- **Pair plot**: a small set of numeric variables; avoid for wide datasets.
- **Correlation heatmap**: compact overview of many pairwise correlations; keep the matrix readable and remember correlation is not causation.

## 2. Deviation

Use when the key message is distance from a baseline, target, zero, benchmark, or prior value.

- **Diverging bar/dot**: signed deviation around a meaningful center.
- **Lollipop**: sparse alternative to bars when exact baseline-to-point distance matters.
- **Area around baseline**: time-indexed positive/negative deviation; use cautiously because filled area visually emphasizes magnitude.

## 3. Ranking

Use when order is the message.

- **Sorted horizontal bar**: default for category ranking.
- **Dot plot**: cleaner than bars when the zero baseline is not meaningful.
- **Lollipop**: acceptable for moderate category counts.
- **Slope chart**: rank/value changes across two or a few ordered states.
- **Dumbbell**: paired values where the gap itself matters.

Always sort intentionally. Do not rely on alphabetical order unless it is meaningful.

## 4. Distribution

Use when the question is shape, spread, skew, tails, overlap, or group differences.

- **Histogram**: default for shape; choose bins deliberately.
- **ECDF**: excellent for cumulative comparison without bin choice.
- **KDE**: smooth shape estimate; avoid when sample size is tiny or boundaries make smoothing misleading.
- **Box plot**: compact robust summary across groups.
- **Violin**: distribution shape plus grouping; more informative with enough observations.
- **Strip/swarm**: individual observations for small-to-medium samples.
- **Ridgeline/joy plot**: many related distributions when overlap is acceptable and ordering is meaningful.
- **Population pyramid**: mirrored distributions for two comparable groups.

## 5. Composition / part-to-whole

Use only when shares of a meaningful whole are central.

- **Stacked bar**: default for absolute composition.
- **100% stacked bar**: compare shares across groups or periods.
- **Treemap**: hierarchical composition when exact comparison is secondary.
- **Waffle**: simple communication of coarse shares, not precise analytical comparison.
- **Pie/donut**: only a few categories with clearly different shares; avoid for close values or many slices.

If the user needs accurate category comparison, use bars instead of area/angle-based charts.

## 6. Change over time

- **Line**: default for continuous chronological change.
- **Step line**: values that change discretely at known boundaries.
- **Line + interval band**: estimate with uncertainty.
- **Multiple lines**: a small number of series with direct labels or a clean legend.
- **Small multiples**: many series or differing shapes.
- **Stacked area**: composition over time when both total and parts matter.
- **Seasonal plot**: repeated within-period patterns across years/cycles.
- **Calendar heatmap**: dense daily activity when day-of-week/calendar structure matters.
- **ACF/PACF or decomposition**: diagnostic time-series analysis, not general-purpose communication.
- **Secondary Y-axis**: last resort; use only when units differ and the mapping is clearly labeled. Prefer aligned panels when possible.

## 7. Groups / structure

- **Facets/small multiples**: safest way to compare the same relationship across groups.
- **Cluster scatter**: show assigned clusters in a low-dimensional projection; make clear whether coordinates are original variables or reduced components.
- **Dendrogram**: hierarchy from clustering; sensitive to distance/linkage choices.
- **Parallel coordinates**: multivariate profiles across a limited number of variables/groups; can become cluttered quickly.
- **Andrews curves**: exploratory multivariate grouping; specialized and rarely the best explanatory chart.

## Avoid-list

Avoid by default:

- 3D bars/pies for ordinary analytical comparisons;
- rainbow palettes without semantic reason;
- dual axes that create a visually convenient but arbitrary relationship;
- pie charts with many slices;
- smoothed curves that obscure raw variability;
- giant pair plots or heatmaps that no longer fit readable labels;
- stacked bars when the user needs to compare non-baseline segments precisely;
- decorative icons/areas whose size is not proportional to the encoded value.
