Let's create a simple line chart. For example, let's plot *sin()* and *cos()* functions on one chart.

Here is our datasource:

```javascript
function data() {
	return (_
      .times(100, function (i) {return i;})
      .reduce(function (memo, x) {
          var i = x / 100;
          return memo.concat([
            {type: 'sin', i: i, val: Math.sin(i)},
            {type: 'cos', i: i, val: Math.cos(i)}
          ]);
      }, []));
}
```

Let's take red line shows *sin()* and green shows *cos()*. Colors brewer is defined in *guide.color.brewer* property.

```javascript
new tauCharts.Chart({
    data: data(),
    type: 'line',
    x: 'i',
    y: 'val',
    color: 'type',
    guide: {
    	color: {
          brewer: { sin: '#ff0000', cos: '#00ff00' }
        }
    }
}).renderTo('#target');
```

See [guide](guide.md) reference for another sophisticated settings.

[Example](http://jsfiddle.net/taucharts/4vgoddao/)

#### split
By default data chunks for a line chart are split by color parameter. Taucharts gives the **split** parameter as an additional way to split data for lines. It is useful when you need to draw separate lines per *property A* and colorize them (optionally) by another *property B*.

Here is an example:

[Example](http://jsfiddle.net/oqyu0j2n/)

#### size
Taucharts allows to build lines of variable width.

Minard's ["Figurative map of the successive losses of men in the French army during the Russian campaign, 1812-1813"](https://en.wikipedia.org/wiki/Charles_Joseph_Minard) is now one of the most famous statistical graphics, thanks to Tufte. Example below demonstrates how to build it using Taucharts:

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

See [size encoding](http://api.taucharts.com/advanced/visual_encoding__size.html) for a details.