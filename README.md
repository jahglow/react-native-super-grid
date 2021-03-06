# React Native Super Grid

Responsive Grid View for React Native.



## Getting Started

This component renders a Grid View that adapts itself to various screen resolutions.

Instead of passing an itemPerRow argument, you pass ```itemDimension``` and each item will be rendered with a dimension size equal to or more than (to fill the screen) the given dimension.

Internally, this component uses the native [FlatList](https://facebook.github.io/react-native/docs/flatlist.html).


### Installing

You can install the package via npm.

```
npm install react-native-super-grid
```

If your react native is below v0.49, install version 1.0.4 - npm install react-native-super-grid@1.0.4


### Usage
```
import GridView from 'react-native-super-grid';
```
```
<GridView
  itemDimension={130}
  items={[1,2,3,4,5,6]}
  renderItem={item => (<Text>{item}</Text>)}
/>
```

#### Properties

| Property | Type | Default Value | Description |
|---|---|---|---|
| renderItem | Function |  | Function to render each object. Should return a react native component. `renderItem` receives object of interface extending `FlatList`'s renderItem argument (`{item, index, separators}`). Additional literals are `rowIndex` and `dimensions` reflecting current measurements for `window`,  `container`, `item`, also has `itemsPerRow`, `spacing`, `fixed` |
| items | Array |  | Items to be rendered. renderItem will be called with each item in this array.  |  |
| keyExtractor | Function |  | Used to extract a unique key for a given item at the specified index. Key is used for caching and as the react key to track item re-ordering. The default extractor checks item.key, then falls back to using the index, like React does.  |  |
| itemDimension (itemWidth if version 1.x.x) | Number | 120  | Minimum width or height for each item in pixels (virtual). |
| fixed | Boolean | false  | If true, the exact ```itemDimension``` will be used and won't be adjusted to fit the screen. |
| spacing | Number | 10 | Spacing between each item. |
| style | [FlatList](https://facebook.github.io/react-native/docs/flatlist.html) styles (Object) |  | Styles for the container. Styles for an item should be applied inside ```renderItem```. |
| staticDimension | Number | undefined | Specifies a static width or height for the GridView container. If your container dimension is known or can be calculated at runtime (via ```Dimensions.get('window')```, for example), passing this prop will force the grid container to that dimension size and avoid the reflow associated with dynamically calculating it|
| aspectRatio| number | undefined | If you want containers wrapping your items maintain aspect ratio automatically and flex content of items fill them, pass a number, e.g if you need aspect ratio of "16:9" pass `aspectRatio={16/9}`. Be aware that this is a canonical aspect ratio (`width:height`) where "16:9" is a landscape orientation of item. if you pass numbers less than zero, you'll get the portrait version of it. Disregarding of `horizontal` or `vertical` scrolling mode for the grid, aspect ratio setting maintains orientation of items in a row (doesn't make "16:9" a "9:16") |
| horizontal | boolean | false | If true, the grid will be scrolling horizontally. Make sure you specify item width in `renderItem` and pass `disableSafetyWidth` OR leave as-is and fall back to column occupying screen width OR use `aspectRatio` to automatically calculate column width|
| disableSafetyWidth | boolean | false | Supplementary to `horizontal` mode only. In `horizontal` mode your items must have a known fixed width, otherwise they collapse to 0 width. If your items do not specify width, safety width (screenWidth - spacing) will be applied to your column. If you want to turn this safety measure off (i.e. your items specify width), set this property to `true`. `aspectRatio` ignores this setting |

Note: If you want your item to fill the height when using a horizontal grid, you should give it a height of '100%'


## Example
```
import React, { Component } from 'react';
import { StyleSheet, View, Text } from 'react-native';
import GridView from 'react-native-super-grid';

export default class Example extends Component {
  render() {
    // Taken from https://flatuicolors.com/
    const items = [
      { name: 'TURQUOISE', code: '#1abc9c' }, { name: 'EMERALD', code: '#2ecc71' },
      { name: 'PETER RIVER', code: '#3498db' }, { name: 'AMETHYST', code: '#9b59b6' },
      { name: 'WET ASPHALT', code: '#34495e' }, { name: 'GREEN SEA', code: '#16a085' },
      { name: 'NEPHRITIS', code: '#27ae60' }, { name: 'BELIZE HOLE', code: '#2980b9' },
      { name: 'WISTERIA', code: '#8e44ad' }, { name: 'MIDNIGHT BLUE', code: '#2c3e50' },
      { name: 'SUN FLOWER', code: '#f1c40f' }, { name: 'CARROT', code: '#e67e22' },
      { name: 'ALIZARIN', code: '#e74c3c' }, { name: 'CLOUDS', code: '#ecf0f1' },
      { name: 'CONCRETE', code: '#95a5a6' }, { name: 'ORANGE', code: '#f39c12' },
      { name: 'PUMPKIN', code: '#d35400' }, { name: 'POMEGRANATE', code: '#c0392b' },
      { name: 'SILVER', code: '#bdc3c7' }, { name: 'ASBESTOS', code: '#7f8c8d' },
    ];

    return (
      <GridView
        itemDimension={130}
        items={items}
        style={styles.gridView}
        keyExtractor={item => item.code}
        renderItem={item => (
          <View style={[styles.itemContainer, { backgroundColor: item.code }]}>
            <Text style={styles.itemName}>{item.name}</Text>
            <Text style={styles.itemCode}>{item.code}</Text>
          </View>
        )}
      />
    );
  }
}

const styles = StyleSheet.create({
  gridView: {
    paddingTop: 25,
    flex: 1,
  },
  itemContainer: {
    justifyContent: 'flex-end',
    borderRadius: 5,
    padding: 10,
    height: 150,
  },
  itemName: {
    fontSize: 16,
    color: '#fff',
    fontWeight: '600',
  },
  itemCode: {
    fontWeight: '600',
    fontSize: 12,
    color: '#fff',
  },
});
```

| ![iPhone6 Portrait](/screenshots/iphone6_portrait.png?raw=true "iPhone6 Portrait")| ![iPhone6 Landscape](/screenshots/iphone6_landscape.png?raw=true "iPhone6 Landscape") |
|:---:|:---:|
| iPhone6 Portrait | iPhone6 Landscape  |

| ![iPad Air 2 Portrait](/screenshots/ipadair2_portrait.png?raw=true "iPad Air 2 Portrait") | ![iPad Air 2 Landscape](/screenshots/ipadair2_landscape.png?raw=true "iPad Air 2 Landscape") |
|:---:|:---:|
| iPad Air 2 Portrait | iPad Air 2 Landscape  |

| ![Android Portrait](/screenshots/android_portrait.png?raw=true "Android Portrait") | ![Android Landscape](/screenshots/android_landscape.png?raw=true "Android Landscape") |
|:---:|:---:|
| Android Portrait | Android Landscape  |

| ![Android Horizontal Portrait](/screenshots/android_horizontal_portrait.png?raw=true "Android Horizontal Portrait") | ![Android Horizontal Landscape](/screenshots/android_horizontal_landscape.png?raw=true "Android Horizontal Landscape") |
|:---:|:---:|
| Android Horizontal Portrait | Android Horizontal Landscape  |

| ![iPhone Horizontal Portrait](/screenshots/iphone_horizontal_portrait.png?raw=true "iPhone Horizontal Portrait")| ![iPhone Horizontal Landscape](/screenshots/iphone_horizontal_landscape.png?raw=true "iPhone Horizontal Landscape") |
|:---:|:---:|
| iPhone Horizontal Portrait | iPhone Horizontal Landscape  |

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.



## Changelog

### [2.2.3] - 2018-03-23
#### Added
- `aspectRatio` maintains aspect ratio of items. This makes item containers of known width and height disregarding of their contents. If you have images of fixed ratio, the content won't 'jump' after they load.
- `horizontal` layout now has a safety measure of setting items width to screen width minus spacing. If your rendered item has explicit width, use `disableSafetyWidth` to disable this measure. `aspectRatio` ignores it. See properties table for more info.

### [2.2.2] - 2018-03-22
#### Improved
- Optimized performance rendering for one-item-in-a-row case 

### [2.2.1] - 2018-03-22
#### Fixed
- `onLayout` is no longer blocking user implementation, instead it calls it after internal use.

### [2.2.0] - 2018-03-22
#### Added
- `renderItem` receives object of interface extending `FlatList`'s renderItem argument (`{item, index, separators}`). 
Additional props are `rowIndex` and `dimensions` reflecting current state measurements.
- Implemented `keyExtractor` to avoid numeric keys if possible. Will fallback to numeric keys when no `keyExtractor` is provided

### [2.1.0] - 2018-03-17
#### Added
- Use FlastList instead of ListView
- Fix spacing issues

### [2.0.2] - 2018-01-11
#### Added
- Allow dynamic update of itemDimension

### [2.0.1] - 2017-12-13
#### Added
- Fixed render empty section headers Warning. @mannycolon

### [2.0.0] - 2017-12-02
#### Added
- Add ability to have a horizontal grid. @Sh3rawi


### [1.1.0] - 2017-11-03 (Target React Native 0.49+)
#### Added
- Replace view.propTypes to ViewPropTypes for 0.49+. @caudaganesh


### [1.0.4] - 2017-10-09
#### Added
- Optional staticWidth prop @thejettdurham.
- Use prop-types package instead of deprecated react's PropTypes.


### [1.0.3] - 2017-06-06
#### Added
- Pass row index to renderItem @heaversm.



## Acknowledgments

Colors in the example from https://flatuicolors.com/.

Screenshot Mockup generated from https://mockuphone.com.
