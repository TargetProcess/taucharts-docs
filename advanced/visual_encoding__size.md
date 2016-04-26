##Size
Using element *size* for encoding can be a powerful visualization technique. If used properly it can give you an immediate insight on your data.

Minard's ["Figurative map of the successive losses of men in the French army during the Russian campaign, 1812-1813"](https://en.wikipedia.org/wiki/Charles_Joseph_Minard) is now one of the most famous statistical graphics, which uses this technique. Here is it in terms of Taucharts API:

```javascript
new tauCharts.Chart({
  type: 'line',
  x: 'longitude',
  y: 'latitude',
  text: 'place',
  size: 'survivors', // we use "size" to encode amount of survivors by line width
  split: 'group',
  color: 'direction',
  data: [...]
})
```
[Example](http://jsfiddle.net/0bu5oo8b/)

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

[Example](http://jsfiddle.net/oLcub5h3/)

#### minSize / maxSize

By default Taucharts tries to infer optimal size scale for a given chart size. While the size scale can be customized by *minSize / maxSize* parameters of *guide.size* section:
- *guide.size.minSize* specifies minimal size of element.
- *guide.size.maxSize* specifies maximal size of element.

**NOTE**: *minSize / maxSize* specify absolute limits for any container size which may look ugly when user resize the chart.

[Example](http://jsfiddle.net/jb87feLj/)