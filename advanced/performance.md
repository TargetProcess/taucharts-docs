## Rendering performance

Drawing big data can be slow.

To prevent browser freeze, several chart settings were introduced in Taucharts v0.10.0:
``` javascript
settings: {
    asyncRendering: false,
    renderingTimeout: 10000,
    syncRenderingInterval: 50,
    handleRenderingErrors: true
}
```

* Setting `asyncRendering: true` will make a chart render asynchronously by small synchronous chunks, making a browser more responsive to user interactions.
* `renderingTimeout` is an interval (ms) after which the rendering will be paused, and user will be prompt to continue or cancel. Setting this option to `0` will disable the pause.
* `syncRenderingInterval` is a minimal interval of synchronous rendering chunks.
* Setting `handleRenderingErrors: false` will make it easier to debug possible rendering errors. Handled errors can be catched using `chart.on('renderingerror', (chart, err) => {...})` event.

Asynchronous rendering prevents browser from freeze, but will not prevent from running out of memory.

[Example](https://jsfiddle.net/6mdLrj6o/21/)