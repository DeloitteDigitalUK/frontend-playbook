# Tools of Trade
_Provides a list of tools that we use in our day-to-day activities._

##Techniques

### Adopt
* **API mocks**  
_API Mocks enable rapid and dependency-free front-end development as we are working in constantly changing environment._

### Trial
* **Pipelines as code**  
_defining the deployment pipeline through code instead of configuring a running CI/CD tool._

* **Architecture decision records**  
_it's important to record certain design decisions for the benefit of future team members and for external oversight. Version controlled markdown suits perfectly. [See Example](https://github.com/npryce/adr-tools/tree/master/doc/adr)_

* **Server-side rendering / Isomorphic apps**

### Assess
* **Micro frontends**  
_a web application is broken up by its pages and features, with each feature being owned end-to-end by a single team._

* **Screenhero**
_Pair programming for remote teams, has slack integration_

### Hold
* TBA


## Libraries / Frameworks

### Adopt
* **classnames**
* **fetch-whatwg**  
_moving away from JQuery or raw XHR for remote JavaScript calls and instead using the new Fetch API and this Fetch polyfill_
* **lodash**
* **moment**
* **react**
* **react-router**
* **redux**
_Predictable client-side state management for complex apps_
* **redux-form@6**
* **redux-thunk**

###Trial
* **vue@2**
* **vuex**

###Assess
* **angular@2**
* **react native**

###Hold
* **angular@1**
* **flux**
* **superagent**  
_Use fetch standardised approach and fetch-whatwg polyfill instead_
* **redux-form@5**

##Tools

###Adopt
* **babel@6**
* **eslint**
* **enzyme**  
_Best in class UI testing tool for React, allows to test without doing on-device rendering_

* **karma**
* **mocha**
* **node-sass**
* **pa11y**  
_Helps to catch a11y issues early, works from command line_
* **redux-devtools**
* **webpack@1**

###Trial
* **immutable.js**  
_useful for returning new instance of app state in a performant way_
* **jest**  
_wasn't a pleasant experience with Jest in 2015, needs to be re-evaluated_
* **ts-loader**
* **tslint**
* **webpack@2**

###Assess
* **galen framework**  
_E2E testing for responsive designs, allows you to specify expectations for the appearance of your website in various screen sizes_
* **grasp**
_Refactoring cli for JS_

### Hold
* **browserify**
* **requireJS**
