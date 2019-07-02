# Smartour

Makes website guiding easier.

## Usage
**Smartour** were built as an `umd` package, which means you can import it in many ways.

```
npm install smartour
```

```javascript
/* ES Modules */
import Smartour from 'smartour'
/* CommandJS */
const Smartour = require('smartour')
/* <script> */
<script src="smartour/dist/index.js"></script>
```

```javascript
const tour = new Smartour().queue([{
  el: '#id',
  slot: `
    <p>Something you want to guide to the visitors</p>
  `
}])

tour.next()
```

## Options
The `Smartour()` is a class who recives an `options` parameter.

```javascript
{
  // `maskStyle` is the stylesheet of the mask.
  // default value will be concated with the new defined.
  markStyle: `
    position: fixed;
    box-shadow: 0 0 0 9999px rgba(0, 0, 0, .5);
    z-index: 9998;
  `, // default

  // `slotStyle` is the stylesheet of the slot content.
  // default value will be concated with the new defined.
  slotStyle: `
    position: fixed;
    z-index: 9999;
  }` // default

  // `maskPadding` sets the padding within the highligt area
  maskPadding: { vertical: 5, horizontal: 5 }, // default

  // `slotPosition` sets the position of the slot content
  // 'top', 'top-right', 'top-left', 'bottom', 'bottom-right', 'bottom-left' are allowd.
  slotPosition: 'bottom', // default

  // `maskEventType` event type of the trigger event binding to the mask
  // 'click', 'mouseon', 'mouseover', 'mousedown', 'mousemove', 'mouseup', 'touchstart', 'touchmove', 'touchend' are allowd
  maskEventType: 'click', //default

  // `maskEvent` is the event binding to the mask
  maskEvent: () => {} // default
```

## APIs
- `queue(TourList)`
  
  `.queue()` recieves a `TourList` parameter, which is a list contains one or more `TourListItem`.

  ```javascript
  [{
    // `el` is the selector of the highlight element
    el: '#id-1',

    // `slot` is a html string of the guide content
    slot: `
      <p>This is a demo...<p>
      <button class="key-1">Cancel</button>
      <button class="key-2">OK</button>
    `,

    // `keyNodes` defines the binding relationship between events and slot
    keyNodes: [{
      el: '.key-1',
      eventType: 'click',
      event: (e) => {
        alert('Click "Cancel" button')
      }
    }, {
      el: '.key-2',
      eventType: 'mouseover',
      event: (e) => {
        alert('Hover "OK" button')
      }
    }]
  }]
  ```

- `next()`

  `.next()` is a function to show the next tour guide, and returns a `Promise` which contains the `Smartour` instance.

  ```javascript
  const tour = new Smartour().queue(TourList)

  await tour.next() // shows the first tour guide
  await sleep(2000) // 2s timeout
  await tour.next() // shows the second tour guide
  ```

- `prev()`

  `.prev()` is a function to show the prev tour guide, and returns a `Promise` which contains the `Smartour` instance.

  ```javascript
  const tour = new Smartour().queue(TourList)

  await tour.next() // shows the first tour guide
  await sleep(2000) // 2s timeout
  await tour.next() // shows the second tour guide
  await sleep(2000) // 2s timeout
  await tour.prev() // shows the first tour guide again
  ```

- `over(smartourInstance)`

  `.over(smartourInstance)` is a function to remove all the guides.

  ```javascript
  const tour = new Smartour().queue(TourList)

  await tour.next() // shows the first tour guide
  await sleep(2000) // 2s timeout

  tour.over(tour) // all the guides were removed
  ```

- `reset(options)`

  Set a new `options` to the `Smartour` instance.

  ```javascript
  const tour = new Smartour().queue(TourList)

  await tour.next() // shows the first tour guide
  await sleep(2000) // 2s timeout

  tour.reset({
    maskStyle: `
      border-radius: 5px;
    `
  })
  tour.next()
  ```

## License
MIT