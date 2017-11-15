# Docker .NET Core Web application
==============================================


A Visual Studio sollution prepared to be used (plug and play) with Docker. It will create 2 contaners, one for the web server and one for the SQL server (both Linux).

----------


Connection to the SQL server (separate container)
-------------


> **Code:** A code example of a SQL connection (MSSQL is located in another container) is located in the following file: *Controllers/HomeController.cs*. The important lines are:

```
SqlConnection cnn;
var connection = @"Server=db;Database=dean;User=sa;Password=ZacetnoGeslo2017+;";
cnn = new SqlConnection(connection);
try
{
    cnn.Open();    
    cnn.Close();
}
catch (Exception ex)
{
}
```

> **Server=db:** "db" is the name of the image instance (container), which is defined in the *docker-compose.yml* defined below.


Insight into docker-compose.yml
-------------
```
version: '3'

services:
  webapplication1:
    image: webapplication1
    build:
      context: ./WebApplication1
      dockerfile: Dockerfile
  db:
    image: "microsoft/mssql-server-linux"
    environment:
      SA_PASSWORD: "ZacetnoGeslo2017+"
      ACCEPT_EULA: "Y"
    ports:
    - "1433:1433"
```
