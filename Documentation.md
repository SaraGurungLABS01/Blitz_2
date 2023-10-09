## Introduction

The task involved deploying a new version of the URL Shortener application and ensuring its capacity to handle a load test with 14,000 concurrent users. The initial evaluation uncovered performance issues when subjected to heavy traffic; , necessitating corrective actions. These issues were successfully addressed, and subsequent testing was conducted on an upgraded instance type, ultimately achieving the desired level of performance.

## Configuration for testing

1) Ensured that the application was running
2) To download the script onto your server, use the following command:

```shell
wget https://raw.githubusercontent.com/kura-labs-org/Template/main/blitz.sh
3) Updating the application.py file:
 - Imported logging
 - In the file or the script, we inserted the following code on line 9 to reconfigure our application. This modification redirected the output from being displayed in the terminal to a file named "app.log" for comprehensive logging:
```shell
logging.basicConfig(filename='app.log', filemode='w', format='%(name)s - %(levelname)s - %(message)s')
