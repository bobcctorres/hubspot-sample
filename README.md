# API Sample Test

## Getting Started

This project requires a newer version of Node. Don't forget to install the NPM packages afterwards.

You should change the name of the ```.env.example``` file to ```.env```.

Run ```node app.js``` to get things started. Hopefully the project should start without any errors.

## Explanations

The actual task will be explained separately.

This is a very simple project that pulls data from HubSpot's CRM API. It pulls and processes company and contact data from HubSpot but does not insert it into the database.

In HubSpot, contacts can be part of companies. HubSpot calls this relationship an association. That is, a contact has an association with a company. We make a separate call when processing contacts to fetch this association data.

The Domain model is a record signifying a HockeyStack customer. You shouldn't worry about the actual implementation of it. The only important property is the ```hubspot```object in ```integrations```. This is how we know which HubSpot instance to connect to.

The implementation of the server and the ```server.js``` is not important for this project.

Every data source in this project was created for test purposes. If any request takes more than 5 seconds to execute, there is something wrong with the implementation.



## Debrief on Improving the Project

Here are some generic considerations that could be be interesting to consider to improve the overall project.

### Code Quality and Readability:

Refactor repeated logic, such as retry mechanisms and pagination handling, into reusable utility functions. This would reduce redundancy and improve maintainability.
Introduce TypeScript or JSDoc comments to define data structures (e.g., meeting objects, attendee objects) and provide better type safety and documentation.
Implement consistent error handling across the codebase using custom error classes to ensure errors are logged and propagated uniformly.
Create centralized logging for Error, Warning and Info logs.

### Project Architecture:

Adopt a modular architecture by grouping related functionalities into separate files or services (e.g., MeetingService, ContactService, etc.). This would isolate concerns and make the project easier to navigate.
Create subfolders for each abstraction concern as well.
Introduce dependency injection to manage external services (e.g., the HubSpot client) more flexibly, making testing and swapping dependencies simpler.
Use environment variables or a configuration manager to handle settings like API keys, retry limits, and endpoint URLs, ensuring they are not hardcoded.


### Code Performance:

Optimize API calls by batching requests wherever possible. For instance, fetching attendees for multiple meetings in a single request (if supported) would reduce latency and network overhead.
Introduce caching (e.g., using Redis) to store frequently accessed or slow-to-fetch data, such as attendee information, to reduce API load.
Parallelize independent operations using asynchronous processing whenever possible.
