# React app structure
## Contents
* [Main folders of the application](#main-folders-of-the-application)
* [File structure](#file-structure)
* [Components](#components)
* [Containers](#containers)
* [Pages](#pages)
* [Redux](#redux)

## Main folders of the application
* **components**: reusable common components
* **containers**: reusable container components
* **layouts**: components that dictate major page structure
* **pages**: all application pages.
* **routes**: React Router routes.
* **store**: Redux store configuration.
* **styles**: application wide styles and variables.
* **utils**: utility & auxiliary functions.  

The **styles** are saved in two places:
* there are **main application styles** that are in the main styles folder
* and the **component specific styles**, that will be kept together with the component (see components, below)

For components, we divide components into the following main categories:

* **reusable components**
	* **components**  
	where we have generic reusable components, that will be shared between more of our components

	* **containers**  
	containers that group actions and logic that needs to be executed across more components
	
* **pages**  
comprising all the actual pages of our application.

	* pages and page specific components that are not used elsewhere.

## File structure
```
public
└── images
src
├── components
├── config
├── containers
├── modules
├── pages
├── routes
├── store
├── styles
└── utils
```

## Components and Containers

### Overview

<table>
    <thead>
        <tr>
            <th></th>
            <th scope="col" style="text-align:left">Presentational Components</th>
            <th scope="col" style="text-align:left">Container Components</th>
        </tr>
    </thead>
    <tbody>
        <tr>
          <th scope="row" style="text-align:right">Purpose</th>
          <td>How things look (markup, styles)</td>
          <td>How things work (data fetching, state updates)</td>
        </tr>
        <tr>
          <th scope="row" style="text-align:right">Aware of Redux</th>
          <td>No</th>
          <td>Yes</th>
        </tr>
        <tr>
          <th scope="row" style="text-align:right">To read data</th>
          <td>Read data from props</td>
          <td>Subscribe to Redux state</td>
        </tr>
        <tr>
          <th scope="row" style="text-align:right">To change data</th>
          <td>Invoke callbacks from props</td>
          <td>Dispatch Redux actions</td>
        </tr>
    </tbody>
</table>

### Components
Should store all reusable components (even if they're currently only used once). These are ideally stateless, state should be handled in the component's container.

#### Naming convention
component name + extension

Here is an example of the file structure that should be used:

```
├── components
│   ├── Header
│   │   ├── Header.js
│   │   ├── Header.scss
│   │   ├── assets
│   │   │   ├── logo-back.jpg
│   │   │   └── logo.png
│   │   └── index.js
```

The component is in a folder of its name. It always has a `.js` file of it's name where the majority of the JavaScript is. It always has a `index.js` file to export the other `js` files. The component relevant `.scss` is here, as well as an assets folder with any images etc. that the component needs. Tests and `storybook` (if used) should also be in the folder.

If you are using typescript, this is where your `.tsx` file will go.


#### Common tasks of a Component
* Should handle any styling or display logic which is based on its props.
* Should change or manipulate data by invoking a callback which is passed as a prop.

### Containers
Should store components which handle state for stateless components. They are either using `state` or connected to the `store`

#### Naming convention
* Container suffix is added to the container file name.  

```
├── containers
│   └── LoginContainer
│   |   ├── LoginContainer.js
│   |   ├── LoginContainer.transformations.js
│   |   └── index.js
```

The component is in a folder of its name. It always has a `.js` or `.tsx` file of its name, as well as an `index.js` file. Optionally, it has a ducks file. (see [Redux](#redux) section)

#### Types

##### Connected to store
* The container will be connected to the `store` and retrieve the required information by using a selector.
* A selector should be used to derive data based on values in the store. `MapStateToProps` is called every time the props have changed and the need to use `componentWillReceiveProps` should be removed. 

Below is an example of how a container can be connected to the store. Selectors should be in their respective ducks folder.

```
const getAddedIds = state => fromCart.getAddedIds(state.cart)
const getQuantity = (state, id) => fromCart.getQuantity(state.cart, id)
const getProduct = (state, id) => fromProducts.getProduct(state.products, id)

export const getTotal = state =>
  getAddedIds(state)
    .reduce((total, id) =>
      total + getProduct(state, id).price * getQuantity(state, id),
      0
    )
    .toFixed(2)

export const getCartProducts = state =>
  getAddedIds(state).map(id => ({
    ...getProduct(state, id),
    quantity: getQuantity(state, id)
  }))


const mapStateToProps = (state) => ({
  products: getCartProducts(state),
  total: getTotal(state)
})
```

##### Fetch Data
* When an API call is needed the container should dispatch an action to request the data. Best practice is to dispatch the action in `componentDidMount`.
* The container should also handle what component is displayed based on loading, error or success state.
* A selector should be used to grab the data/error from state once the API call is in progress/has finished/has error.
* One approach is to have a generic container responsible for API calls - displaying an error, loading screen or a container once the call has finished successfully. Then the second container will be connected the store and grab the required information. In this way, we will have a separation of concerns where one container is doing API calls and the other grabbing the required information from the store.


#### Summary of container's tasks
* Request the data (invoke a subscription or just fetch it).
* Show a loading screen while the data is being fetched.
* Once the data arrives, pass it to the UI component.
* If there is an error, show it to the user.
* It may need to refetch or re-subscribe when props change.
* It needs to clean up resources (like subscriptions) when the container is unmounting.

## Pages
Should store pages. These are slim files which only have either containers or components in them.  
Pages are page specific components, not used elsewhere and are linked to a specific route via react-router. 

### Naming convention
Page suffix is added to the page file name

```
├── pages
│   └── HomePage.js
```

Each page is just a `.js` or `.ts` files, no folder required.

### Common tasks of a Page
* Link to a URL
* Group components together

## Tests
Test files live in the same folder as their testing counterpart. Test files should be suffixed with `.spec.js`.


## Redux

### Structure and Naming

[Use Ducks](https://github.com/erikras/ducks-modular-redux)

**action name**: NOUN_VERB  
**action creator name**: verbNounAction
**action creator thunk** verbNoun
**selector name**: getNoun  

### Rules
* Your __reducers__ must be pure (__deterministic__).
* Use Immutable to ensure that your are not mutating the state in your reducers. Remember, `{...state}` is only a shallow copy!
* Any logic with side effects (__non-deterministic__) (external services, async code) belong in an action (via something like [redux-thunk](https://github.com/gaearon/redux-thunk) and/or [redux-saga](https://github.com/yelouafi/redux-saga))
  * For more about the deterministic vs non-deterministic, see [this](https://github.com/reactjs/redux/issues/1171#issuecomment-205888533) Github Issue response.
* Containers read a store's data through selectors. Selectors are your "reading API" and should be __co-located__ with their reducers.
  * See [So you’ve screwed up your Redux store — or, why Redux makes refactoring easy](https://blog.boldlisting.com/so-youve-screwed-up-your-redux-store-or-why-redux-makes-refactoring-easy-400e19606c71#.rho2ned2d)
  * [Computing Derived Data | Redux](http://redux.js.org/docs/recipes/ComputingDerivedData.html)
  * [Colocating Selectors with Reducers](https://egghead.io/lessons/javascript-redux-colocating-selectors-with-reducers)
* __Use selectors everywhere__. Even for the most trivial ones.
* Redux should store the minimal possible state, allowing Selectors to compute derived data.
* Use [Reselect](https://github.com/reactjs/reselect) for selectors that need to be memoized (like derived data).
* `mapState`should run as fast as possible.
  * if using immutable, DO NOT call `toJS()` in a `mapState`
  * from [Practical Redux, Part 6: Connected Lists, Forms, and Performance · Mark's Dev Blog](http://blog.isquaredsoftware.com/2017/01/practical-redux-part-6-connected-lists-forms-and-performance/)
* Selectors can be composed of other selectors
* Normalize your data for better reducer composition
  * see the output of [normalizr](https://github.com/paularmstrong/normalizr) for an example
