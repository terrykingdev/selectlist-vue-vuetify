# SelectList vue-vuetify component

A vuetify list component to replace the html SELECT which doesn't render as expected on mobile devices. This demo features two lists where items from the left can be added to or removed from the list on the right. Selected items on the right can also be moved up and down.

The SelectList component needs two lists. 'list' is an array of objects, one property needs to be 'text' which will be used to display the text. 'selectedList' is an array of indexes of highlighted items. Highlight items with a single click, or to select multiple hold down Control, or hold down Shift to select a range.

```html
<SelectList
    :list="availableOutputFields"
    :selectedList="availableOutputFieldsSelected"
    />
```
```javascript
  data: function(){
    return {
      availableOutputFieldsSelected: [],
      availableOutputFields: [
        { text: 'Antenna Port', value: 'antennaport'},
        { text: 'Timestamp', value: 'timestamp'},
        { text: 'Peak RSSI', value: 'rssi'},
        { text: 'TID', value: 'tid'},
        { text: 'User Memory', value: 'usermem'},
        { text: 'EPC', value: 'epc'}
      ],
     }
  },
```

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
