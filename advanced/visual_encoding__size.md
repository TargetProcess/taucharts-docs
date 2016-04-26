##Size
Apply *size encoding* by assigning measure variable to **size** parameter.

The *size* encodes visually:
- width of bar for a (stacked) bar chart
- diameter of point for a scatter chart
- variable line width for a line chart
- diameter of anchor point for an area chart.

The element size is customized by min / max parameters of *guide.size* section.

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
