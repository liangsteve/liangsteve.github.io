---
layout: default
title: Vega-Lite Demo
---

## Vega-Lite Chart Example

This is a simple bar chart embedded in a Jekyll Markdown page using Vega-Lite.

<div id="vis" style="width: 100%; max-width: 600px;"></div>

<script src="https://cdn.jsdelivr.net/npm/vega@5"></script>
<script src="https://cdn.jsdelivr.net/npm/vega-lite@5"></script>
<script src="https://cdn.jsdelivr.net/npm/vega-embed@6"></script>

<script type="text/javascript">
  const spec = {
    "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
    "description": "A simple bar chart.",
    "data": {
      "values": [
        {"category": "A", "value": 28},
        {"category": "B", "value": 55},
        {"category": "C", "value": 43},
        {"category": "D", "value": 91},
        {"category": "E", "value": 81}
      ]
    },
    "mark": "bar",
    "encoding": {
      "x": {"field": "category", "type": "ordinal"},
      "y": {"field": "value", "type": "quantitative"}
    }
  };

  vegaEmbed('#vis', spec);
</script>
