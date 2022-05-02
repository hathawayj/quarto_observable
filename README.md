# Quarto with Observable Plot

_Experiments using [observable plot](https://observablehq.com/@observablehq/plot) ([repo](https://github.com/observablehq/plot)) within the new [Quarto notebooks](https://quarto.org/)_

- [JavaScript for Python Programmers](https://observablehq.com/@ballingt/javascript-for-python-programmers)
- [Quarto and Observable JS](https://quarto.org/docs/interactive/ojs/)
- [Quarto Visual Editor](https://quarto.org/docs/visual-editor/)
- [Quarto Using Python](https://quarto.org/docs/computations/python.html)
- [Altair with Quarto](https://jjallaire.github.io/visualization-curriculum/)
- [Moving data from Python/R to OJS](https://quarto.org/docs/interactive/ojs/#data-sources)

> Yes, you can do this using the ojs_define() function (available in both Python and R): https://quarto.org/docs/interactive/ojs/#data-sources
> [JJ Allaire's Response](https://github.com/quarto-dev/quarto-cli/issues/749#event-6513759255)

```{python}
import pandas as pd
penguins = pd.read_csv("palmer-penguins.csv")
ojs_define(data = penguins)
```

The call to `ojs_define(data = penguins)` says that we want to make a variable named data (with the value of the `penguins` data frame) available to OJS

Depending on the visualization library you use, one additional step may be required to consume the data from JavaScript. In this case, the Plot function expects data by row rather than by column, so we `transpose()` it before filtering:

```{ojs}
filtered = transpose(data).filter(function(penguin) {
  return bill_length_min < penguin.bill_length &&
         islands.includes(penguin.island);
})
```

See the article on [Data Sources](https://quarto.org/docs/interactive/ojs/data-sources.html) to learn more about the various ways to prepare and read data.