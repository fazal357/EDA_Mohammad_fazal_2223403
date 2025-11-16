# EDA_Mohammad_fazal_2223403
EDA Final Assignment

# Deploy a pre-built module to the Edge device:

## 1. Created an Azure Resource Group 
The first step was setting up a Resource Group in Azure. 
A Resource Group acts as a container to organize all the cloud resources we create. I created a dedicated resource group so that the IoT Hub and device identity are isolated and easy to manage. 
  
## 2. Created an IoT Hub 
Next, I created an Azure IoT Hub, which is the cloud control center for managing IoT devices. 
This hub: 
•	securely registers devices 
•	sends configuration to IoT Edge devices 
•	collects telemetry from modules 
•	handles cloud-to-edge messaging 
I used the standard setup and created an IoT Hub inside the resource group. 
  
## 3. Registered an IoT Edge Device 
Inside the IoT Hub, I went to Devices → Add Device, and enabled the IoT Edge option. 
This generated a device identity in the cloud with: 
•	Device ID 
•	Primary Key 
•	Connection Strings 
I copied the IoT Edge device’s primary connection string so I could use it during runtime configuration. 
  
## 4. Set Up IoT Edge Runtime on my Laptop (WSL2 Ubuntu 20.04) 
Since I did not have physical IoT hardware, I converted my laptop into a simulated IoT Edge device using WSL2 Ubuntu. 
I installed: 
•	Microsoft packages 
•	Azure IoT Identity service 
•	Docker Engine 
•	Azure IoT Edge Runtime 
Then I configured the device using: 
sudo iotedge config mp --connection-string "<device-connection-string>" sudo iotedge config apply 
This successfully linked my WSL Linux environment to Azure IoT Hub as a functioning IoT Edge device. 
  
## 5. Started IoT Edge Runtime 
I started the runtime: 
sudo systemctl start aziot-edged This launched: 
•	edgeAgent (module manager) 
•	edgeHub (message broker) I confirmed they were running using: sudo iotedge list 
  
## 6. Deployed Modules Using Azure CLI 
Instead of using the portal UI, I used Azure CLI for clean deployment. 
I created a deployment.json file containing the configuration for: 
•	$edgeAgent 
•	$edgeHub 
•	the SimulatedTemperatureSensor module 
•	routing from sensor to IoT Hub 
Then deployed it to my device: 
az iot edge set-modules \ 
  --hub-name Faz-hub \ 
  --device-id edgeDevice1 \ 
  --content deployment.json 
Azure IoT Hub immediately pushed the deployment to my WSL IoT Edge device. 
  
## 7. Verified the Three Modules Running 
I checked the status: 
sudo iotedge list Output confirmed: 
•	edgeAgent → running 
•	edgeHub → running 
•	SimulatedTemperatureSensor → running 
This shows the deployment succeeded. 
  
## 8. Viewed Real-Time Telemetry Output 
To show the data flow, I streamed module logs: iotedge logs SimulatedTemperatureSensor -f 
This displayed telemetry every 5 seconds, including: 
•	machine temperature 
•	pressure 
•	ambient temperature 
•	humidity 
•	timestamp 
For example: 
Sending message: 1, Body: {"machine": {"temperature": 21.1 ...}} 
This confirmed: 
•	the module is generating sensor data 
•	the device is functioning as an IoT Edge gateway 
•	data is flowing through edgeHub to the cloud 
  
#  Final Summary 
1.	Made a Resource Group 
2.	Created an IoT Hub 
3.	Registered an IoT Edge device 
4.	Installed IoT Edge runtime on WSL2 Linux 
5.	Configured the device using connection string 
6.	Deployed a prebuilt module using Azure CLI 
7.	Verified modules with iotedge list 
8.	Showed live telemetry from the simulated temperature sensor 
This completes the hands-on demonstration for Module 3 of the AI Edge Engineer path.” 
  
If you want, I can format this into a short 1-minute version or a presentation slide. 
 
