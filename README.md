# react-router-primitives
Create cross-platform app routing for React web, React Native and react-sketchapp.

(work in progress and unstable API). Please wait for 0.1.0 release as a minimum for a more stable API.

## Getting Started

```sh
npm i -S react-router-primitives
```

## API

```js
module.exports = {
  Router,
  Route,
  Link,
  Switch,
  withRouter,
}
```

### Exported Components and Methods


### `<Router>`

A universal router component that uses `<BrowserRouter>` on web, `<SketchRouter>` on React Sketch.app and `<NativeRouter>` on React Native. Thanks to [ReactTraining/react-router](https://github.com/ReactTraining/react-router/).

#### Props

| Prop        | Type                          | Default      | Note |
| ----------- | ----------------------------- | ------------ | --- |
| `location`  | [`string`]    \| [`Location`]  | **required** | String or Location e.g. `{ key: 'ac3df4', pathname: '/somewhere', search: '?some=search-string', hash: '#howdy', state:  [userDefined]: true } }` |
| `locations` | [`string[]`] \| [`Location[]`]  | **required** | List of strings or locations |
| `viewport`  | [`viewport`]                   | **required** | Object: { name: string, width: number, height: number}  |
| `children`  | [`Node`]                       | **required** |            |

#### Example

```js
import sketch from 'sketch';
import { Router, Route, Switch } from 'react-router-primitives';
import { RedBox, render } from 'react-sketchapp';

const pageWidth = ...;

// Multi-platform app component (can be imported from component library or other file)
const App = () => (
    <Router
      locations={['/profile/john']}
      viewport={viewports}
    >
      <Switch>
        <Route exact path="/" render={() => <Home />} />
        <Route path="/about" render={() => <About />} />
        <Route path="/profile/:username" render={({ match: { params } }) => <Profile {...params} />} />
        <Route component={NotFound} />
      </Switch>
    </SketchRouter>
  </Page>
);

// Sketch entry-point
export default () => {
  const { selectedPage } = sketch.getSelectedDocument();
  try {
    render((
      <Page name="App" style={{ flexDirection: 'row', flexWrap: 'wrap', maxWidth: pageWidth }}>
        <App />
      </Page>
    ), selectedPage);
  } catch (err) {
    render(<RedBox error={err} />, selectedPage);
  }
};
```
