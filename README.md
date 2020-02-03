# react-map-usa | A simple SVG USA map rendering on React

[![Build Status](https://travis-ci.org/ljmerza/react-map-usa.svg?branch=master)](https://travis-ci.org/ljmerza/react-map-usa)

This is an alternate version for you that just want a simple customizable map on HTML. This maps shows states delimitations including DC, Alaska, and Hawaii. D3 is not needed.

It uses the [Albers projection](https://en.wikipedia.org/wiki/Albers_projection).

## [Live Example](http://react-usa-map-demo.herokuapp.com)
Live: [http://react-usa-map-demo.herokuapp.com](http://react-usa-map-demo.herokuapp.com)

Code: [https://github.com/ljmerza/react-map-usa](https://github.com/ljmerza/react-map-usa)

## Installation

It requires `react` 15.4.2 or higher, compatible with React 16.0.0. Run:

`yarn add react-map-usa`

or

`npm install react-usa-map --save`

## Usage

```javascript
import React, { Component } from 'react';
import USAMap from "react-map-usa";

class App extends Component {
  mapHandler = (event) => {
    alert(event.target.dataset.name);
  };

  render() {
    return (
      <div className="App">
        <USAMap onClick={this.mapHandler} />
      </div>
    );
  }
}

export default App;
```

Example with optional props, `App.js`:

```javascript
import React, { Component } from 'react';
import './App.css'; /* optional for styling like the :hover pseudo-class */
import USAMap from "react-usa-map";

class App extends Component {
  mapHandler = (event) => {
    alert(event.target.dataset.name);
  };

  /* optional customization of filling per state and calling custom callbacks per state */
  statesCustomConfig = () => {
    return {
      "NJ": {
        fill: "navy",
        clickHandler: (event) => console.log('Custom handler for NJ', event.target.dataset)
      },
      "NY": {
        fill: "#CC0000"
      }
    };
  };

  render() {
    return (
      <div className="App">
        <USAMap customize={this.statesCustomConfig()} onClick={this.mapHandler} />
      </div>
    );
  }
}

export default App;
```

`App.css`:

```css
path {
  pointer-events: all;
}
path:hover {
  opacity: 0.50;
  cursor: pointer;
}
```

## All optional props:

|prop|description|
|----|-----------|
|`title`| Content for the Title attribute on the `svg`|
|`width`| The `width` for rendering, numeric, no `px` suffix|
|`height`| The `height` for rendering, numeric, no `px` suffix|
|`defaultFill`| The default color for filling|
|`customize`| Optional customization of filling per state |
|`onClick`| Optional onclick event on a state |
|`onMouseOver`| Optional onmouseover event on a state |

Additionally each `path` tag has an abbreviation of the current state followed by a `state` class:

```html
<path fill="#{custom color or #D3D3D3}" data-name="CA" class="CA state" d="...{polygon dimensions here}..."></path>
```

# License

[MIT](LICENSE.md).

# Sources

The map is sourced from [Wikimedia](https://commons.wikimedia.org/wiki/File:Blank_US_Map_(states_only).svg) and is under [Creative Commons Attribution-Share Alike 3.0 Unported](https://spdx.org/licenses/CC-BY-SA-3.0.html) license. This package is inspired on the [react-us-state-map](https://npmjs.com/package/react-map-usa) package, in fact the initial SVG class system is based on it.
