# API Testing Project - Restful-Booker

# API-Testing-Project-1

Reference Urls:

https://restful-booker.herokuapp.com/apidoc/index.html

https://www.postman.com/automation-in-testing/workspace/restful-booker-collections/overview

https://github.com/mwinteringham/restful-booker

Introduction

This document provides detailed documentation for the Restful-Booker API, covering various endpoints for managing bookings. 

The API allows users to perform operations such as creating, retrieving, updating, and deleting bookings.

Base URL

https://restful-booker.herokuapp.com

Authentication

To access certain endpoints, authentication is required. The CreateToken endpoint is used to generate an authentication token, which should be included in subsequent requests.
CreateToken



POST /auth

Creates a new authentication token.
Example Usage:



curl -X POST \
  https://restful-booker.herokuapp.com/auth \
  -H 'Content-Type: application/json' \
  -d '{
    "username" : "admin",
    "password" : "password123"
}'

Request Headers:

    Content-Type: application/json

Request Body:

    username: Username for authentication
    password: Password for authentication

Success Response (200):

json

{
    "token": "abc123"
}

Endpoints
GetBookingIds



GET /booking

Returns the IDs of all the bookings that exist within the API. Can take optional query strings to search and return a subset of booking IDs.
Example Usage:



curl -i https://restful-booker.herokuapp.com/booking

Parameters:

    firstname (optional): Return bookings with a specific firstname
    lastname (optional): Return bookings with a specific lastname
    checkin (optional): Return bookings that have a checkin date greater than or equal to the set checkin date (Format: CCYY-MM-DD)
    checkout (optional): Return bookings that have a checkout date greater than or equal to the set checkout date (Format: CCYY-MM-DD)

Success Response (200):

json

[
  {
    "bookingid": 1
  },
  {
    "bookingid": 2
  },
  {
    "bookingid": 3
  },
  {
    "bookingid": 4
  }
]

GetBooking



GET /booking/:id

Returns a specific booking based upon the booking ID provided.
Example Usage:



curl -i https://restful-booker.herokuapp.com/booking/1

URL Parameter:

    id: The ID of the booking you would like to retrieve

Success Response (200):

json

{
    "firstname": "Sally",
    "lastname": "Brown",
    "totalprice": 111,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2013-02-23",
        "checkout": "2014-10-23"
    },
    "additionalneeds": "Breakfast"
}

CreateBooking



POST /booking

Creates a new booking in the API.
Example Usage:


curl -X POST \
  https://restful-booker.herokuapp.com/booking \
  -H 'Content-Type: application/json' \
  -d '{
    "firstname" : "Jim",
    "lastname" : "Brown",
    "totalprice" : 111,
    "depositpaid" : true,
    "bookingdates" : {
        "checkin" : "2018-01-01",
        "checkout" : "2019-01-01"
    },
    "additionalneeds" : "Breakfast"
}'

Request Headers:

    Content-Type: application/json

Success Response (200):

json

{
    "bookingid": 1,
    "booking": {
        "firstname": "Jim",
        "lastname": "Brown",
        "totalprice": 111,
        "depositpaid": true,
        "bookingdates": {
            "checkin": "2018-01-01",
            "checkout": "2019-01-01"
        },
        "additionalneeds": "Breakfast"
    }
}

UpdateBooking



PUT /booking/:id

Updates a current booking.
Example Usage:

bash

curl -X PUT \
  https://restful-booker.herokuapp.com/booking/1 \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Cookie: token=abc123' \
  -d '{
    "firstname" : "James",
    "lastname" : "Brown",
    "totalprice" : 111,
    "depositpaid" : true,
    "bookingdates" : {
        "checkin" : "2018-01-01",
        "checkout" : "2019-01-01"
    },
    "additionalneeds" : "Breakfast"
}'

Request Headers:

    Content-Type: application/json
    Accept: application/json
    Cookie (optional): Sets an authorization token to access the PUT endpoint

URL Parameter:

    id: ID for the booking you want to update

Success Response (200):

json

{
    "firstname" : "James",
    "lastname" : "Brown",
    "totalprice" : 111,
    "depositpaid" : true,
    "bookingdates" : {
        "checkin" : "2018-01-01",
        "checkout" : "2019-01-01"
    },
    "additionalneeds" : "Breakfast"
}

PartialUpdateBooking



PATCH /booking/:id

Updates a current booking with a partial payload.
Example Usage:



curl -X PATCH \
  https://restful-booker.herokuapp.com/booking/1 \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Cookie: token=abc123' \
  -d '{
    "firstname" : "James",
    "lastname" : "Brown"
}'

Request Headers:

    Content-Type: application/json
    Accept: application/json
    Cookie (optional): Sets an authorization token to access the PATCH endpoint

URL Parameter:

    id: ID for the booking you want to update

Success Response (200):

json

{
    "firstname" : "James",
    "lastname" : "Brown",
    "totalprice" : 111,
    "depositpaid" : true,
    "bookingdates" : {
        "checkin" : "2018-01-01",
        "checkout" : "2019-01-01"
    },
    "additionalneeds" : "Breakfast"
}

DeleteBooking



DELETE /booking/:id

Deletes a booking.
Example Usage:



curl -X DELETE \
  https://restful-booker.herokuapp.com/booking/1 \
  -H 'Content-Type: application/json' \
  -H 'Cookie: token=abc123'

Request Headers:

    Content-Type: application/json
    Cookie (optional): Sets an authorization token to access the DELETE endpoint

URL Parameter:

    id: ID for the booking you want to delete

Success Response (201):

HTTP/1.1 201 Created

Ping
HealthCheck



GET /ping

A simple health check endpoint to confirm whether the API is up and running.
Example Usage:



curl -i https://restful-booker.herokuapp.com/ping

Success Response (200):

HTTP/1.1 201 Created

Conclusion

This concludes the documentation for the Restful-Booker API. Users can utilize these endpoints to manage bookings effectively. For any further assistance or queries, please refer to the provided reference URLs.


# Generating HTML Report for Postman Collection Using Newman and Postman CLI

To create an HTML report for your Postman collection execution results, you can utilize Newman or Postman CLI. This guide outlines the steps to execute your collection and generate a detailed HTML report using these command-line tools.

# To generate an HTML report for your Postman collection using Newman and Postman CLI, follow these steps:

1. Install Newman

If you haven't already installed Newman, you can do so using npm (Node Package Manager). Run the following command in your terminal or command prompt:

npm install -g newman

2. Export Your Postman Collection

Export your Postman collection as a JSON file. You can do this by opening Postman, selecting your collection, clicking on the ellipsis (...) menu, and choosing "Export". Save the collection as a JSON file.

3. Run Your Collection Using Newman

Now, run your collection using Newman. Use the following command in your terminal or command prompt:


newman run your_collection.json -r html

Replace your_collection.json with the path to your exported collection JSON file. -r html option is used to specify that you want Newman to generate an HTML report.

4. Specify Report Output Path

If you want to specify the output path for the HTML report, you can use the -o option followed by the desired path:



newman run your_collection.json -r html -o report.html

5. Access the HTML Report

Once Newman has finished running your collection, you'll find the HTML report generated at the specified output path. You can open this HTML file in any web browser to view the detailed report of your collection run.

# Using Postman CLI

Alternatively, you can also use the Postman CLI to run your collection and generate the HTML report. Postman CLI is integrated with Newman, so the process is quite similar.

1. Install Postman CLI

You can install Postman CLI using npm:

npm install -g postman-cli

2. Run Your Collection Using Postman CLI

Run your collection using Postman CLI:


postman run your_collection.json --reporter html --reporter-html-export report.html

Replace your_collection.json with the path to your exported collection JSON file. --reporter html option specifies that you want to generate an HTML report. --reporter-html-export report.html specifies the output path for the HTML report.

3. Access the HTML Report

Once Postman CLI finishes running your collection, you'll find the HTML report generated at the specified output path (report.html). You can open this HTML file in any web browser to view the detailed report of your collection run.

Following these steps, you'll be able to run your Postman collection using Newman or Postman CLI and generate an HTML report for the results.

# Fixing "newman: could not find 'html' reporter" Error: Installation and Rerun Steps

If you encounter the error "newman: could not find 'html' reporter" while trying to run your collection with Newman, follow these steps to fix the issue:
Question:

What does the error "newman: could not find 'html' reporter" mean?
Answer:

This error indicates that Newman is unable to find the HTML reporter, which is required to generate HTML reports for your collection runs.
Solution:

    Install Newman HTML Reporter: Run the following command in your terminal or command prompt to install the HTML reporter globally:



npm install -g newman-reporter-html

Rerun Your Collection: Once the HTML reporter is installed, rerun your collection command:


    newman run Restful-Booker.postman_collection.json -r html

    Permission Consideration: Ensure that you have the necessary permissions to install npm packages globally. If you encounter permission errors, you may need to use sudo (on Unix-based systems) or run your command prompt as an administrator (on Windows).

 #    file:///C:/Users/pc/Downloads/newman/newman-run-report-2024-04-06-13-50-09-900-0.html 
    

By following these steps, you should be able to resolve the issue and generate HTML reports for your Postman collection runs using Newman.

# Fixing "'postman' is not recognized" Error and Running Postman Collection Using Postman CLI

If you're encountering the error "'postman' is not recognized as an internal or external command" while attempting to use Postman CLI,

it suggests that the Postman CLI executable is not found in your system's PATH.

To fix this issue and use Postman CLI successfully, you can try the following steps:

    Ensure Postman CLI is Installed:
    Verify that Postman CLI is installed on your system. You can install it using npm:

npm install -g postman-cli

Check System PATH:

Ensure that the directory where Postman CLI is installed is added to your system's PATH environment variable. This allows your system to locate the Postman CLI executable.

You can check the PATH variable in your system's environment settings.

Restart Command Prompt or Terminal:

After installing Postman CLI and updating the PATH variable, close and reopen your command prompt or terminal. This ensures that the changes to the PATH variable take effect.

Verify Installation:

Run the command postman --version in your command prompt or terminal. If Postman CLI is correctly installed and added to your PATH, this command should display the version of Postman CLI installed.

Retry Command:

Once you've verified that Postman CLI is installed and added to your PATH, retry running your command:



    postman run Restful-Booker.postman_collection.json --reporter html --reporter-html-export report.html

By following these steps, you should be able to fix the issue and run your Postman collection using Postman CLI successfully.

# Choose between Newman and Postman CLI for your API testing needs. 

Here's a comprehensive comparison incorporating the latest information and real-world examples:

Newman

    Purpose: Newman is a free, open-source command-line tool specifically designed to run Postman collections. It excels at integrating seamlessly with CI/CD pipelines for automated testing.
    
    Advantages:
        CI/CD Integration: Newman integrates effortlessly with popular CI/CD platforms like Jenkins, GitLab CI/CD, CircleCI, and Travis CI using shell scripts or pre-built integrations. This allows you to automate API testing as part of your development workflow. (Example: In a Jenkins pipeline, you can use the sh step to execute Newman with your Postman collection file.)
        Scripting Flexibility: Newman offers extensive command-line options and scripting capabilities using JavaScript or Node.js. This empowers you to customize test execution, handle complex scenarios, and integrate with other tools for a more robust testing environment. (Example: You can write a script to conditionally execute certain tests based on environment variables or test results.)
        Large Community: Newman boasts a large and active open-source community, providing ample resources and support for troubleshooting and customization. (Example: You can find helpful discussions and solutions on the Newman GitHub repository or forums like Stack Overflow.)
    Use Cases:
        Automated API testing in CI/CD pipelines.
        Integration testing to verify API interactions with other components.
        Performance testing by measuring API response times under load (often in conjunction with additional tools).

Postman CLI

    Purpose: Introduced in 2021, Postman CLI is a command-line interface directly tied to the Postman API. It offers a convenient way to interact with Postman features and execute collections from the command line.
    Advantages:
        Postman Ecosystem Integration: Postman CLI integrates seamlessly with other Postman features, allowing you to leverage monitoring, mocks, environments, and more directly from the command line. This simplifies your workflow and reduces context switching. (Example: You can use the postman pm:monitor command to start monitoring an API endpoint after running a collection with Newman.)
        Simplified Execution: Postman CLI is generally easier to use for basic tasks compared to Newman's scripting-heavy approach. It provides quick access to Postman features, making it ideal for manual testing or ad-hoc collection execution. (Example: You can use the postman collection run command to quickly run a collection without needing complex scripting.)
  
    Use Cases:
        Manual testing of API collections.
        Quick execution of collections for debugging or exploratory testing.
        Running collections as part of a larger workflow that leverages other Postman features (e.g., monitoring changes in an API after a collection run).

Decision Factors:

    Complexity of Testing:
        Newman: If you need complex scripting, conditional logic, or advanced integrations with CI/CD pipelines, Newman offers greater flexibility.
        Postman CLI: If your testing needs are more straightforward and don't require extensive scripting, Postman CLI might be a simpler choice.
    Integration with Other Tools:
        Newman: Newman excels at integrating with various tools and platforms beyond Postman due to its open-source nature.
        Postman CLI: Postman CLI prioritizes seamless integration within the Postman ecosystem.
    Ease of Use:
        Newman: Newman has a steeper learning curve due to its command-line and scripting nature.
        Postman CLI: Postman CLI offers a more user-friendly experience for basic use cases, especially for those already familiar with Postman.

In Conclusion:

Both Newman and Postman CLI are valuable tools for API testing. The best choice depends on your specific requirements and preferences. Consider the factors above to make an informed decision:

    For complex automated testing, intricate scripting, and flexibility in CI/CD pipelines, choose Newman.
    For straightforward manual testing, rapid collection execution, and seamless integration with the Postman ecosystem, choose Postman CLI.

Remember, you can experiment with both tools to determine which one aligns best with your workflow.
