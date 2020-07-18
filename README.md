# stm-azurertos-workshop
For STM Azure RTOS workshop
- STM32CubeIDE
- b-l475e-iot01a discovery board

Project source : https://github.com/azure-rtos/samples/releases
- Azure_RTOS_6.0_STM32L475-DISCO_STM32CubeIDE_Samples_2020_05_17.zip
- follow Azure_RTOS_STM32L475-DISCO_Azure_IoT_Quick_Connect_For_STM32CubeIDE.pdf

Steps:
1. > git clone https://github.com/sha1painkiller/stm-azurertos-workshop.git
2. Create Azure IoT Hub for demo
- IoT Hub -> Setting -> Shared access policies -> iothubowner -> Connection string
- save Connection String for later use
3. Install Azure IoT Explorer - https://docs.microsoft.com/en-us/azure/iot-pnp/howto-install-iot-explorer
- get credential (the connection string) to activate Azure IoT Explorer
- create a new IoT device
- copy Device ID for later use
- copy connection string with SAS token for later use (starts from SharedAccessSignature sr=.)
4. Launch STM32CubeIDE
5. Open Project From File System -> "stm-azurertos-workshop" and find "sample_azure_iot" project.
6. Find board_setup.c under "common_hardware_code"
- configure SSID and password
7. Find sample_azure_iot\sample_azure_iot.c
- configure HOST_NAME / DEVICE_ID / DEVICE_SAS
8. Build the project
- right click sample_azure_iot project, and select Property -> Project References
- choose "nx_secure" / "nxd" / "stm32l475_lib" / "tx"
- project -> build
9. Run -> Debug (F11)
10. open Termite (or other terminals) to observe the device log
- temperature growing on the device
11. Monitor Telemetry data on Azure IoT Explorer
12. Send message from cloud to device
- {"fan" : "on"}
- temperature decreasing on device





