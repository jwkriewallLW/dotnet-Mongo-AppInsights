# Dotnet-Mongo-AI
Dotnet webapi -> MongoDB -> AppInsights

--STRUCTURE--
This project was built to test the relationship between a dotnet application, MongoDB and Application Insights. A movie playlist can be modified with CRUD operations using a sample dotnet app (with an accompanying web UI). The results of the modifications are stored in a sample MongoDB Atlas instance. Finally, logs are collected by dotnets ILogger framework and sent to Application Insights.

PREREQUISITES: Dotnet 6.0, MongoDB Atlas, an Azure Application Insights instance. Linux perspective.

--Dotnet Sample Application Install--
Make sure dotnet 6.0 is installed.
Initialized in CLI with command: dotnet new webapi

The above command installs a sample DotNet application "Weather Forecast" which spits out randomized weather. It will serve as the basis through which we create the new application. Follow this walkthrough if you'd like more information on the changes I made to the original code to produce the current Movie template: https://www.mongodb.com/developer/how-to/create-restful-api-dotnet-core-mongodb/

--CONNECTION STRINGS--
![image](https://user-images.githubusercontent.com/83727077/158868592-c424337c-eb07-4e63-8fcc-f515cd3e95f0.png)
There are a few connection strings that you will need to procure: One from Mongo and one from App Insights.
For the Mongo Connection String, press the Connect button and choose to the "Connect your application" option. Select the driver and version (for this code, use the drop down to select 'C# / .NET' and 'Version 2.13 or later'). 
![image](https://user-images.githubusercontent.com/83727077/158864579-5cd02e23-c735-4994-93f1-14e1e97427a5.png)
Copy the connection string which will look a bit like this: mongodb+srv://<username>:<password>@sandbox.skl1b.mongodb.net/<Database_Name>?retryWrites=true&w=majority
Before inserting into the code, you'll need to add your username and password as well as the database you're trying to connect to. IMPORTANT - in Mongo, a collection is a sub database. Make sure you are clear on what you'll be connecting to. In our case, we will connect to the "Sample_mflix" database, so you can replace <Database_Name> with sample_mflix. 
If you need a reminder of your Username or password, check the Database Access tab on the side of the MongoDB Atlas Interface.
  ![image](https://user-images.githubusercontent.com/83727077/158868258-48469ce7-c15c-4618-b262-186d94b6cfca.png)
Now head over to the appsettings.json file and insert into the "MongoDB" area.
  
For Application Insights, you can find the instrumentation key on the home page of your resource group. Copy the Instrumentation Key, and input it into the appsettings.json file in the "Application Insights" area. 
  
--LOGGING--
Logs will be automatically generated from the current code - find all instances in the Playlist Controller.cs file. 
An example of a logging message would be _logger.LogInformation($"This is a sample log");
In PlaylistController.cs, the ILogger is passed through the PlaylistController Constructor. Then, _logger can be used in the code anywhere in the Constructor. Explore the different messages that will be applied when a CRUD operation is run. These messages will show in App Insights as traces. I am currently experimenting with how to register Information messages and lower into AI as currently it only shows warnings and above.
