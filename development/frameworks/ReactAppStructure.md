#React app structure
## Contents
* [Main folders of the application](#main-folders-of-the-application)
* [File structure](#file-structure)
* [Components](#components)
* [Containers](#containers)
* [Pages](#pages)
* [Tests](#tests)

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
tests
├── components
├── containers
├── modules
├── pages
├── store
└── utils
```

## Components
Should store all reusable components (even if they're currently only used once!). These are ideally stateless, state should be handled in the component's container.

### Naming convention
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

The component is in a folder of its name. It always has a `.js` file of it's name where the majority of the JavaScript is. It always has a `index.js` file to export the other js file. The component relevant `.scss` is here optionally, as well as an assets folder with any images etc. that the component needs.

If you are using typescript, this is where your `.tsx` file will go.

### Common tasks of a Component
TBA

## Containers
Should store smart components which handle state for stateless components.

### Naming convention
* Container suffix is added to the container file name.  
* Ducks suffix is added to the ducks file.

```
├── containers
│   └── Login
│   |   ├── LoginContainer.js
│   |   ├── LoginDucks.js
│   |   └── index.js
```

The component is in a folder of its name. It always has a `.js` or `.ts` file of its name, as well as an `index.js` file. Optionally, it has a ducks file.

### Common tasks of a Container
* A container’s main task is to fetch the data. For that, it has to do a few things:
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
Test files live in a separate folder outside of the main folder, which replicates the src folder. Test files should be suffixed with `.spec.js`.

```
tests
├── components
│   └── HeaderComponent.spec.js
```
