## Introduction

The task involved deploying a new version of the URL Shortener application and ensuring its capacity to handle a load test with 14,000 concurrent users. The initial evaluation uncovered performance issues when subjected to heavy traffic; 3864 of them encountered failure, necessitating corrective actions. These issues were successfully addressed, and subsequent testing was conducted on an upgraded instance type, ultimately achieving the desired level of performance.

## Configuration for testing

1) Ensured that the application was running in port 5000
2) To download the script onto your server, use the following command:

```shell
wget https://raw.githubusercontent.com/kura-labs-org/Template/main/blitz.sh
```
3) Updating the application.py file:
 - Imported logging
 - In the file or the script, we inserted the following code on line 9 to reconfigure our application. This modification redirected the output from being displayed in the terminal to a file named "app.log" for comprehensive logging:
```shell
logging.basicConfig(filename='app.log', filemode='w', format='%(name)s - %(levelname)s - %(message)s')
```
![image](https://github.com/SaraGurungLABS01/Blitz_2/assets/140760966/00d37a65-fe60-472a-949b-711ac43895b8)



4) Comitted the changes in the repository Deployment_4

5) The application was deployed on an EC2 instance of the t2.micro type. However, it's important to note that the t2 instance family, including t2.micro, is known for its burstable CPU performance, which may not be ideal for sustaining high loads due to its CPU credits system.

6) **Configuring nginx**
   
   ![image](https://github.com/SaraGurungLABS01/Blitz_2/assets/140760966/962f9493-e93e-4889-9b26-e5fe25d32edf)

   
To address the above issue, we took steps to optimize Nginx, the web server used in our setup, to effectively receive and process more incoming requests. Specifically, we configured Nginx to utilize 8 worker processes. These worker processes are responsible for handling incoming connections and requests, allowing Nginx to efficiently distribute the workload.

In addition, we increased the maximum number of connections that Nginx can accept to 2000. This adjustment significantly improved Nginx's capacity to handle concurrent connections and enabled it to better receive and process a higher volume of incoming requests.

While these configurations enhanced the server's ability to manage incoming web traffic and requests, it's important to remain mindful of the limitations of t2 instances, including t2.micro, which rely on the burstable CPU credit mechanism. 

![image](https://github.com/SaraGurungLABS01/Blitz_2/assets/140760966/36ca58cb-fd39-49e0-8f1c-a93036c09d34)

**Enabling Gzip compression setting**

To further bolster web server performance and enhance page loading speed, we activated Gzip compression within Nginx. This enhancement compresses content before transmission, reducing data size during transit.

![image](https://github.com/SaraGurungLABS01/Blitz_2/assets/140760966/77cf3732-f660-490c-9d98-132703b39355)

7) Installed a package for stress testing: Executed `sudo apt install stress-ng` to install the required package for stress testing.

8) Added a shell script for stress testing: Introduced a shell script containing the following code: `sudo nice -n -20 stress-ng --cpu 2`. This script is meticulously crafted to conduct stress tests on two CPUs, assigning them high priority to achieve optimal results.

![image](https://github.com/SaraGurungLABS01/Blitz_2/assets/140760966/486522b4-3216-4b36-8978-13dbe5a5e84c)


## Initial test Result

During the QA testing, out of the 14,000 concurrent requests initiated to stress test the application, 3,864 requests did not pass, indicating the need for further investigation and optimization.

## Steps to remediate the Issue





