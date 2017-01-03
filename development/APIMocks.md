#API Mocks
##Aim
The aim of using mocks is to replicate specific API calls without modifying application code. i.e. developer should be able to switch mock API on and off as I needed. Ideally, an application can be developed and run in an "airplane" mode, without any 3rd party dependencies. This will enable rapid and dependency free front-end development.

##Consistency
To achieve consistency in implementation we strongly suggest to base mocks on [openAPI](https://www.openapis.org/specification/repo) standard and make sure that other systems use the same contracts.

OpenAPI contracts need to be defined in code, utilise version control and be maintained by all involved parties to ensure consistent and compatible format for describing APIs, allowing interoperation between tooling, systems, and runtime environments.


##Rationale
1. **No API yet.** A mocked API allows you to begin development without waiting for the API team to build the services you need. And if you haven’t decided how to design your web services, mocking allows you to rapidly prototype different potential response shapes to see how they work with your app.

2. **Slow or unreliable API.** Are the existing APIs in your dev or QA environment slow, unreliable, or expensive to call? If so, a mocked API offers consistent, instantaneous responses for rapid feedback development. And if your existing web services go down, a mocked API allows you to keep working.

3. **Eliminate inter-team dependencies.**  Is a separate team creating your app’s web services? A mocked API means you can start coding immediately and switch to the real web services when they’re ready. Just agree on the API’s proposed design and mock it accordingly.

4. **Work offline.** Finally, maybe you need to work on a plane, on the road, or in other places where connectivity is poor. Mocking allows you to work offline because your calls remain local.

##Online
* [Apigee](https://apigee.com/)
* [apiary](https://apiary.io/)

##Offline
* [Imposter](https://github.com/outofcoffee/imposter)
* [Swagger](http://swagger.io/)