##Size
Size encoding currently applies to point element only. Point diameter depends on the min and max value in a *size* dimension.

```javascript
var spec = {
    unit:[{
        type: 'ELEMENT.POINT',
        x: 'effort',
        y: 'cycleTime',
        size: 'bugsCount'
    }]
};
```

[Example](http://jsfiddle.net/taucharts/awn8rz8w/)
