##What is TauCharts?
TauCharts is a javascript charting library. It is based on the awesome [D3 framework](http://d3js.org/) and [Grammar of Graphics](http://www.amazon.com/The-Grammar-Graphics-Statistics-Computing/dp/0387245448) concepts.

We built TauCharts around three rules:

1. Graphical design is imporant, so we design everything with passion.
2. Simple charts are easy to create, complex charts are not easy, but possible.
3. Flexibility is important. Its [plugins framework](../plugins/README.md) should be powerful.

##How do I create a simple line chart?

You have to include the d3.js, underscore, and taucharts libraries:

```html
<script src="//cdn.jsdelivr.net/d3js/latest/d3.min.js" charset="utf-8"></script>
<script src="//cdn.jsdelivr.net/taucharts/latest/tauCharts.min.js" type="text/javascript"></script>
```

Also include the TauCharts CSS file:

```html
<link rel="stylesheet" type="text/css" href="//cdn.jsdelivr.net/taucharts/latest/tauCharts.min.css">
```

Then [prepare your data](../datasource/README.md) for use with the library. TauCharts accepts data as an array of similarly-typed objects (it looks like CSV):


```javascript
var datasource = [{
  type:'us', count:20, date:'12-2013'
},{
  type:'us', count:10, date:'01-2014'
},{
  type:'bug', count:15, date:'02-2014'
},{
  type:'bug', count:23, date:'05-2014'
}];
```

The actual chart definition is pretty simple and speak for itself:

```javascript
var chart = new tauCharts.Chart({
    data: datasource,
    type: 'line',
    x: 'date',
    y: 'count',
    color: 'type' // there will be two lines with different colors on the chart
});
```

Then, you can render the chart into some HTML element (container):

```html
<div id='line'>
```

You can reference container using selector or pass a DOM element:

```javascript
chart.renderTo('#line');
// or
chart.renderTo(document.getElementById('#line'));
```

[Example jsFiddle](https://jsfiddle.net/taucharts/u86cseky/)

Now, find 5 free minutes and [check out our extended tutorial](5min.md).

