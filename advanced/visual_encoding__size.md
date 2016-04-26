##Size
Apply *size encoding* by assigning measure variable to **size** parameter.

The *size* encodes visually:
- width of bar for a (stacked) bar chart
- diameter of point for a scatter chart
- variable line width for a line chart
- diameter of anchor point for an area chart.

```javascript
new tauCharts.Chart({
  type: 'scatterplot',
  x: 'cycleTime',
  y: 'effort',
  size: 'bugsCount',
  data: [...]
})
```

[Example](http://jsfiddle.net/7qon6mkg/)

By default Taucharts tries to infer optimal size scale for a given chart size. While the size scale can be customized by *minSize / maxSize* parameters of *guide.size* section:
- *guide.size.minSize* specifies minimal size of element.
- *guide.size.maxSize* specifies maximal size of element.

NOTE: minSize / maxSize specify absolute limits for any container size which may look ugly when user resize the chart.