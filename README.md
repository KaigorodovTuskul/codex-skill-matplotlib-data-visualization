# Matplotlib Data Visualization

A Codex skill for selecting, building, improving, and auditing analytical visualizations in Python with Matplotlib and optional Seaborn.

The skill is inspired by the analytical taxonomy behind **“The Master Plots”**: correlation, deviation, ranking, distribution, composition, change, and groups. It does **not** copy the historical code examples verbatim; instead it translates the underlying chart-selection logic into a modern workflow and uses current Matplotlib-style object-oriented patterns.

## What it does

- identifies the analytical question before choosing a chart;
- maps the question to an appropriate visualization family;
- inspects data types, dates, missingness, ordering, units, and aggregation before plotting;
- prefers simple, interpretable charts over decorative ones;
- generates modern Matplotlib code and uses Seaborn selectively;
- handles time series, ranking, distributions, correlation, part-to-whole, uncertainty, and grouped comparisons;
- audits axes, scales, labels, color, accessibility, transformations, and output quality;
- modernizes old plotting snippets instead of preserving deprecated APIs.

## Structure

```text
.
|- SKILL.md
|- agents/
|  `- openai.yaml
`- references/
   |- chart-selection.md
   |- implementation-patterns.md
   `- qa-checklist.md
```

## Installation

Current Codex user-scoped location:

### macOS / Linux

```bash
git clone <REPOSITORY_URL> ~/.codex/skills/matplotlib-data-visualization
```

### Windows PowerShell

```powershell
git clone <REPOSITORY_URL> "$env:USERPROFILE\.codex\skills\matplotlib-data-visualization"
```

If your existing setup discovers skills from `~/.agents/skills/`, the same repository can be placed there instead.

Invoke explicitly with:

```text
$matplotlib-data-visualization
```

or let Codex discover it from the task description.

## Example requests

```text
$matplotlib-data-visualization
I have monthly plan/fact data by business line. Choose the best chart and create a presentation-ready PNG.
```

```text
$matplotlib-data-visualization
Review this Matplotlib code. The chart feels misleading and the labels overlap. Fix it without changing the underlying data.
```

```text
$matplotlib-data-visualization
Build a clear visualization of the relationship between duration and yield, with issuer groups highlighted.
```

## Design notes

The historical Habr article used Matplotlib 3.0.0 and Seaborn 0.9.0 in its setup. The skill therefore treats the article as a visualization catalogue and decision framework, not as a compatibility baseline. It instructs Codex to check installed versions and rewrite old snippets against supported APIs.

Primary references used while designing the skill:

- Habr translation: https://habr.com/ru/articles/468295/
- Original “Top 50 matplotlib Visualizations”: https://machinelearningplus.com/plots/top-50-matplotlib-visualizations-the-master-plots-python/
- Matplotlib documentation: https://matplotlib.org/stable/
- Seaborn documentation: https://seaborn.pydata.org/
- OpenAI Skills documentation: https://developers.openai.com/api/docs/guides/tools-skills

## License

No license has been assigned. Add one before redistributing the repository if you want to grant reuse rights explicitly.
