# rcepjs-most

> Most.js dependencies.

## Install

npm (comming soon):
```sh
npm install --save rcepjs-most
```

browser:
```html
<script src="path_to_cepjs-core/dist/rcepjsMost.min.js"></script>
```

### CommonJS
```JavaScript
const coreFactory = require('rcepjs');
const { merge, fromEvent, tumblingTimeWindow, all, EventType } = coreFactory(require('rcepjs-most'));

let clickStream = fromEvent(document, 'click',
    domEvent => new EventType('click event', 'DOM', Date.now()));

let keyPressStream = fromEvent(document, 'keypress',
    domEvent => new EventType('key press event', 'DOM', Date.now()));

let subscription =
      merge(clickStream, keyPressStream)
        .pipe(tumblingTimeWindow(1000),
          all(['click event', 'key press event'], 'click & press'))
        .subscribe({
          next: derivedEvent =>
            console.log(`Detected at ${new Date(derivedEvent.detectionTime)}`)
        });
```
### IIFE (browser)
```JavaScript
const { merge, fromEvent, tumblingTimeWindow, all, EventType } = rcepjs(rcepjsMost);

let clickStream = fromEvent(document, 'click',
    domEvent => new EventType('click event', 'DOM', Date.now()));

let keyPressStream = fromEvent(document, 'keypress',
    domEvent => new EventType('key press event', 'DOM', Date.now()));

let subscription =
      merge(clickStream, keyPressStream)
        .pipe(tumblingTimeWindow(1000),
          all(['click event', 'key press event'], 'click & press'))
        .subscribe({
          next: derivedEvent =>
            console.log(`Detected at ${new Date(derivedEvent.detectionTime)}`)
        });
```