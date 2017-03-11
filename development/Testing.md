# Testing

Writing tests before writing code is a skill. It may appear hard at first, but it gets better with practice. The result of that effort is a more modular, cohesive, and loosely coupled design.

Tests are also a form of documentation. Unlike traditional documentation or specifications, they are live and active documentation that verify code’s behavior with each change.

A good way to incrementally develop code is through a series of positive, negative, and exception tests. 

- **Positive** tests exercise and verify that the code does what’s expected when its preconditions are met.
- **Negative** tests verify that the code gracefully behaves when things don’t go as expected—that is, when its preconditions or input are not valid.
- **Exception** tests verify that if code is supposed to throw an exception, it does in fact.

## FAIR Principle
When thinking of tests, think of keeping them FAIR:
- **Fast** 
  Fast tests mean fast feedback loops. If tests are slow, you’ll be tempted to run them less often.

- **Automated**
  A major benefit of tests is verification, it should be automated and not be manual.
  
- **Isolated**  
  Isolated tests can be run in any order, and you can also run a select few of them as you desire or all of them. No test should require that any other test be run before it—such tests are brittle and turn into time sinks.
  
- **Repeatable**  
  Tests should be repeatable; you should be able to run them any number of times without needing manual or time-consuming setup or cleanup operations.
  
## Client-side specifics
When testing client-side codewe also need to consider the following aspects
- Works well in all target browsers
- Interacts properly with the server
- Correctly acts on user commands

## Types of tests

- **Unit test**  
  If you are testing one small module of your application, you are writing a unit test. You’ll need to stub and mock other modules that your module usually leverages in order to isolate each test. You’ll typically also need to spy on actions that the module takes to verify that they occur.

- **Integration test**  
  If you are testing that multiple modules behave properly, you are writing an integration test. Such tests are much more complex and may require running code both on the client and on the server to verify that communication across that divide is working as expected. Typically an integration test will still isolate a part of the entire application and directly verify results in code.

- **Acceptance test**  
  If you want to write a test that can be run against any running version of your app and verifies at the browser level that the right things happen when you push the right buttons, then you are writing an acceptance test (sometimes called “end to end test”). Such tests typically try to hook into the application as little as possible, beyond perhaps setting up the right data to run a test against.

- **Load test**  
  Finally you may wish to test that your application works under typical load or see how much load it can handle before it falls over. This is called a load test or stress test. Such tests can be challenging to set up and typically aren’t run often but are very important for confidence before a big production launch.
