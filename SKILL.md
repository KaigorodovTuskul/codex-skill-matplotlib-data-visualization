---
name: matplotlib-data-visualization
description: "Choose, build, improve, and audit analytical charts in Python with Matplotlib and optional Seaborn. Use when the user needs a chart from data, help selecting the right visualization, production-quality plotting code, or a review of an existing plot for clarity, accuracy, and readability."
---

# Matplotlib Data Visualization

Use this skill when the task is to turn data into an analytical chart, choose a chart type, improve an existing visualization, or write/review Matplotlib/Seaborn plotting code.

The workflow is inspired by the seven visualization objectives used in *The Master Plots*: correlation, deviation, ranking, distribution, composition, change, and groups. Treat those as analytical intents, not as a requirement to reproduce a particular gallery example.

## Core rules

1. Start from the analytical question, not from a chart type. Identify what the user is trying to compare, explain, detect, rank, or monitor.
2. Inspect the data before plotting. Resolve column meanings, units, data types, missing values, duplicates, date parsing, category order, aggregation level, and obvious outliers that can change the visual conclusion.
3. Classify the primary visual objective using [references/chart-selection.md](references/chart-selection.md). If several objectives apply, choose one primary chart and add secondary views only when they answer a distinct question.
4. Prefer the simplest chart that preserves the relevant structure. Do not use an exotic chart merely because it is available.
5. Prefer Matplotlib's object-oriented interface (`fig, ax = plt.subplots(...)`, then `ax.*`). Use Seaborn when it materially simplifies statistical aggregation, faceting, categorical plots, regression, or distribution plots.
6. Do not copy old plotting snippets blindly. Check the installed library versions when compatibility matters and use currently supported APIs. Historical examples written for older Matplotlib/Seaborn versions may contain deprecated calls or obsolete argument styles.
7. Never distort the message with inappropriate axis limits, unequal category spacing, truncated bars without an explicit reason, hidden missing data, or inconsistent scales across comparable panels.
8. Encode the main comparison with position or length before relying on area, angle, color intensity, or decorative effects. Avoid 3D charts for ordinary analytical work.
9. Use color deliberately. One highlight color is usually enough; use categorical palettes for unordered groups, sequential palettes for magnitude, and diverging palettes only around a meaningful midpoint. Do not rely on red/green alone when accessibility matters.
10. Label the chart so it can stand on its own: descriptive title, units, axis labels where needed, source/note when relevant, legend only when direct labels are not cleaner.
11. When uncertainty exists and is material, show it with error bars, intervals, ribbons, or another explicit encoding. Do not imply precision the data does not support.
12. For time series, preserve chronological order, use real datetime values, avoid categorical date spacing, and show gaps rather than silently connecting missing periods unless interpolation is explicitly intended.
13. For many categories, sort them, abbreviate carefully, wrap labels, use horizontal orientation, or show the top/bottom subset with an explicit note. Do not produce unreadable label walls.
14. For composition, default to stacked or 100% stacked bars when comparison matters. Use pie, waffle, or treemap only when part-to-whole is the actual question and their perceptual trade-offs are acceptable.
15. For dense scatter data, consider transparency, smaller markers, hexbin/binning, density views, or faceting rather than plotting an opaque cloud.
16. Keep transformations explicit. If you normalize, standardize, smooth, aggregate, resample, winsorize, log-transform, or calculate rolling statistics, state it in code and in the chart note/title when it affects interpretation.

## Workflow

### 1. Frame the question

Determine:

- target audience and medium: notebook, report, slide, dashboard, publication, or exploratory analysis;
- analytical intent: correlation, deviation, ranking, distribution, composition, change, or groups;
- key dimensions and measures;
- whether the task is exploratory or explanatory;
- whether the user requires a specific chart type, style, size, file format, or library.

If the user's requested chart is unsuitable, preserve the request when it is explicit but briefly flag the limitation and, when useful, provide a better alternative.

### 2. Inspect and prepare the data

Before plotting:

- print or inspect shape, columns, dtypes, head/tail, missingness, and unique counts for categorical fields;
- parse dates and numeric fields deliberately;
- verify units and aggregation level;
- sort ordered categories and time;
- decide whether aggregation belongs in the chart code or upstream;
- avoid mutating the user's source data unnecessarily; work on a copy for chart-specific transformations.

### 3. Select the chart

Read [references/chart-selection.md](references/chart-selection.md) when the chart type is not already fixed. Use its decision matrix and avoid-list.

Typical defaults:

- relationship between two numeric variables -> scatter;
- dense numeric relationship -> hexbin/density or transparent scatter;
- category comparison/ranking -> sorted horizontal bar or dot plot;
- paired before/after comparison -> dumbbell or slope chart;
- one numeric distribution -> histogram, ECDF, or box/violin depending on the question;
- time evolution -> line chart;
- uncertainty over time -> line + interval band;
- part-to-whole -> stacked/100% stacked bar before pie/waffle/treemap;
- correlation matrix -> heatmap when the number of variables remains readable;
- many comparable groups -> small multiples/facets;
- hierarchical clustering -> dendrogram only when the hierarchy itself matters.

### 4. Implement

Read [references/implementation-patterns.md](references/implementation-patterns.md) for modern reusable patterns.

Prefer:

- `fig, ax = plt.subplots(...)`;
- explicit variables for figure size and output path;
- `constrained_layout=True` or a deliberate layout strategy for multi-panel figures;
- `ax.set(...)`, `ax.tick_params(...)`, `ax.legend(...)`, and direct artist handles;
- `fig.savefig(..., bbox_inches="tight")` only after checking that the final layout is correct;
- vector output (`.svg`/`.pdf`) for diagrams/reports when appropriate, high-DPI `.png` for raster delivery.

Use helper functions when the same formatting or transformation repeats. Keep chart code deterministic and reproducible.

### 5. Audit the result

Read [references/qa-checklist.md](references/qa-checklist.md) before final delivery for non-trivial charts.

At minimum verify:

- chart answers the stated question;
- axes, scales, units, and baseline are not misleading;
- category/time order is correct;
- labels are legible and not clipped;
- legend entries match plotted series;
- annotations do not overlap important marks;
- color meaning is consistent and accessible;
- no important data was silently dropped;
- aggregation/transformation is visible in code and explained when material;
- output file opens correctly and is visually inspected when the environment allows it.

## Output behavior

When the user asks for plotting code, return runnable code with the minimum necessary explanation.

When the user asks you to create the chart from available data, produce the chart file and the code used to generate it when feasible. Briefly state the chart choice and any material transformation.

When reviewing an existing chart, separate issues into: analytical choice, data/aggregation, scale/encoding, layout/readability, and implementation/API. Fix the chart rather than merely criticizing it when the data/code is available.

When several chart types are plausible, do not dump a gallery. Recommend one primary option and at most one meaningful alternative unless the user explicitly asks for variants.

## Boundaries

- Do not fabricate missing data, categories, confidence intervals, or statistical relationships.
- Do not infer causality from correlation or visual co-movement.
- Do not hide inconvenient observations simply to make a cleaner chart.
- Do not use a decorative visualization when it weakens quantitative comparison.
- Do not force Seaborn, Plotly, Altair, or another library when the user explicitly asked for Matplotlib-only output.
