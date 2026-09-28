# Visualization QA Checklist

Use this for any chart that will be delivered, published, or used in a decision.

## Analytical fit

- What exact question does the chart answer?
- Is the chosen chart the simplest good representation of that question?
- Does the visual emphasize the intended comparison rather than a decorative feature?
- If a statistical model or smoother is shown, is its role clear and justified?

## Data integrity

- Correct rows, filters, dates, units, categories, and aggregation level?
- Missing values handled explicitly?
- Duplicates checked where they would double-count?
- Transformations reproducible in code?
- No silent exclusion of outliers or inconvenient observations?

## Scales and encoding

- Bars use an honest baseline unless a break/truncation is explicitly signaled?
- Log scale labeled and appropriate for the data?
- Comparable panels use comparable scales when comparison is intended?
- Diverging scales have a meaningful midpoint?
- Marker area, line width, and color intensity are not implying unsupported quantitative meaning?

## Readability

- Title states the point or subject clearly?
- Units are visible?
- Labels fit without clipping or excessive rotation?
- Legend is necessary, correct, and ordered consistently with the visual?
- Direct labels used when they reduce eye travel?
- Gridlines support reading rather than dominate?
- Annotation count is restrained?

## Accessibility

- Main distinctions remain understandable without relying only on red vs green?
- Contrast is sufficient?
- Small text remains readable in the target medium?
- Colorblind-safe or redundant encodings used when the audience requires it?

## Output

- Correct aspect ratio for notebook/report/slide?
- Raster output has adequate DPI?
- Vector output used where useful?
- File opens correctly?
- Final rendered result visually inspected when possible?
