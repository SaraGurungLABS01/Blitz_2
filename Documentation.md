## Introduction

The task at hand revolved around deploying an updated version of the URL Shortener application while ensuring its capability to accommodate a substantial load of 14,000 concurrent users. Initial evaluation exposed performance issues when subjected to a high influx of traffic, with 3,864 requests encountering failures, prompting the need for corrective measures. These challenges were effectively addressed, leading to subsequent testing on an upgraded instance type that ultimately achieved the desired level of performance.

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

CPU usage spiked at  100%


![image](https://github.com/SaraGurungLABS01/Blitz_2/assets/140760966/bf9a7682-fb9e-4ef5-91fd-84a3341d5870)


## Steps to remediate the Issue

During the initial load testing, it became evident that the URL Shortener application may have been grappling with the expected traffic load. Among the 14,000 concurrent requests initiated for stress testing, a substantial portion, precisely 3,864 requests, encountered difficulties, resulting in failures. Additionally, CPU usage peaked at 100%. These observations led to speculation that the choice of the t2.micro EC2 instance type for hosting the application might be a contributing factor to these performance challenges. To mitigate this issue, the prospect of upgrading to the t2.xlarge instance type was considered. Given the performance limitations encountered with the t2.micro instance during the initial load testing, it is advisable to proceed with the upgrade to the t2.xlarge instance type. In contrast to the t2.micro's single vCPU and 1 GB of memory, the t2.xlarge presents four vCPUs and 16 GB of memory, resulting in a substantial boost in computational power and memory resources. This upgrade ensures the application's ability to adeptly manage the anticipated 14,000 concurrent users while remaining cost-effective, striking an optimal balance between heightened performance and budgetary considerations.

 **Steps to change the instance type in the console**
1) Ensure your instance is not running.
2) Navigate to the EC2 console and click on "Actions."
3) Select "Change instance settings."
4) Choose your desired instance type to initiate the upgrade process.

## Expected result after the upgrade

Following the upgrade to the t2.xlarge instance type, it is anticipated that the server will effectively manage 100% of the anticipated traffic without encountering errors. This upgrade equips the application to confidently handle the expected load, ensuring a seamless user experience.






   









