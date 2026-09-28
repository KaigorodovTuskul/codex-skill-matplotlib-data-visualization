# Modern Matplotlib Implementation Patterns

These are patterns, not mandatory styling. Adapt to the user's data and house style.

## Base pattern

```python
import matplotlib.pyplot as plt

fig, ax = plt.subplots(figsize=(10, 6), constrained_layout=True)

# ax.plot(...), ax.bar(...), ax.scatter(...), etc.

ax.set(
    title="Descriptive title",
    xlabel="X label",
    ylabel="Y label, units",
)
ax.grid(axis="y", alpha=0.25)

fig.savefig("chart.png", dpi=200)
plt.show()
```

Prefer the object-oriented API so multi-panel figures and reusable functions remain predictable.

## Sorted horizontal ranking

```python
plot_df = df[["category", "value"]].dropna().sort_values("value")

fig, ax = plt.subplots(figsize=(9, 6), constrained_layout=True)
ax.barh(plot_df["category"], plot_df["value"])
ax.set(title="Ranking by value", xlabel="Value", ylabel="")
ax.grid(axis="x", alpha=0.25)
```

## Scatter with optional fitted line

Use raw points first. Add a fit only when it answers the question and the model assumption is defensible.

```python
fig, ax = plt.subplots(figsize=(8, 6), constrained_layout=True)
ax.scatter(df["x"], df["y"], alpha=0.6, s=28)
ax.set(title="Y vs X", xlabel="X", ylabel="Y")
ax.grid(alpha=0.2)
```

For large datasets, consider `ax.hexbin(...)` rather than opaque scatter points.

## Histogram

```python
values = df["value"].dropna()

fig, ax = plt.subplots(figsize=(9, 5), constrained_layout=True)
ax.hist(values, bins="auto", edgecolor="white")
ax.set(title="Distribution of value", xlabel="Value", ylabel="Count")
```

Choose bins deliberately when business interpretation depends on thresholds or known intervals.

## Time series

```python
plot_df = df[["date", "value"]].dropna().copy()
plot_df["date"] = pd.to_datetime(plot_df["date"])
plot_df = plot_df.sort_values("date")

fig, ax = plt.subplots(figsize=(11, 5), constrained_layout=True)
ax.plot(plot_df["date"], plot_df["value"], linewidth=1.8)
ax.set(title="Value over time", xlabel="", ylabel="Value")
ax.grid(axis="y", alpha=0.25)
```

Do not convert dates to arbitrary integer positions unless there is a specific reason.

## Time series with uncertainty

```python
fig, ax = plt.subplots(figsize=(11, 5), constrained_layout=True)
ax.plot(df["date"], df["estimate"], label="Estimate")
ax.fill_between(
    df["date"],
    df["lower"],
    df["upper"],
    alpha=0.2,
    label="Interval",
)
ax.legend(frameon=False)
```

State what the interval means (for example, 95% confidence interval, prediction interval, min-max band).

## Multi-panel small multiples

```python
fig, axes = plt.subplots(
    nrows=len(groups),
    ncols=1,
    figsize=(10, 2.5 * len(groups)),
    sharex=True,
    constrained_layout=True,
)

for ax, group in zip(axes, groups):
    part = df[df["group"] == group]
    ax.plot(part["date"], part["value"])
    ax.set_title(str(group), loc="left")
    ax.grid(axis="y", alpha=0.2)
```

Keep comparable scales aligned unless the analytical reason for separate scales is explicit.

## Heatmap

For correlation or compact matrices, Seaborn is acceptable when available:

```python
import seaborn as sns

corr = df[numeric_cols].corr()
fig, ax = plt.subplots(figsize=(9, 7), constrained_layout=True)
sns.heatmap(corr, ax=ax, cmap="vlag", center=0, square=True)
ax.set_title("Correlation matrix")
```

Do not annotate every cell when the matrix is too large to read.

## Version compatibility

Before using specialized or recently changed APIs:

```python
import matplotlib
print(matplotlib.__version__)

try:
    import seaborn as sns
    print(sns.__version__)
except ImportError:
    sns = None
```

If an example found online targets old releases, rewrite it against the installed version rather than suppressing warnings or pinning obsolete dependencies without a user requirement.
