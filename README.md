# stm-azurertos-workshop
For STM Azure RTOS workshop
- STM32CubeIDE
- b-l475e-iot01a discovery board

Project source : https://github.com/azure-rtos/samples/releases
- Azure_RTOS_6.0_STM32L475-DISCO_STM32CubeIDE_Samples_2020_05_17.zip
- follow Azure_RTOS_STM32L475-DISCO_Azure_IoT_Quick_Connect_For_STM32CubeIDE.pdf

Steps:
1. git clone https://github.com/sha1painkiller/stm-azurertos-workshop.git
2. Create Azure IoT Hub for demo
- IoT Hub -> Setting -> Shared access policies -> iothubowner -> Connection string
- save Connection String for later use
3. Install Azure IoT Explorer - https://docs.microsoft.com/en-us/azure/iot-pnp/howto-install-iot-explorer
- get credential (the connection string) to activate Azure IoT Explorer
- create a new IoT device
- copy Device ID for later use
- generate a SAS connection string with 180-minutes validity
- copy the generated SAS token for later use (starts with SharedAccessSignature sr=.)
4. Launch STM32CubeIDE and create a workspace for the project (in the same git local repository)
5. File -> Open Project from File System -> "stm-azurertos-workshop" and click "finish"
6. In "sample_azure_iot" project, find board_setup.c under "common_hardware_code"
- configure WIFI_SSID and WIFI_PASSWORD
7. Find sample_azure_iot\sample_azure_iot.c
- configure HOST_NAME / DEVICE_ID / DEVICE_SAS (SAS string starts with "SharedAccessSignature sr=.....")
8. Build the project
- right click sample_azure_iot project, and select Property -> Project References
- choose "nx_secure" / "nxd" / "stm32l475_lib" / "tx"
- Project -> Build All (Ctrl-B)
9. Run -> Debug (F11) (ps. make sure the Wi-Fi AP or hotspot is truned ON)
10. Open Termite (or other terminals) to observe the device log
- temperature starts growing (from 21 and capped at 40) on the device
11. Monitor Telemetry data on Azure IoT Explorer
12. Send message from cloud to device (to cool down the device)
- On Azure IoT Explorer, "Cloud-to-device message"
- put {"fan" : "on"} on Message body and click "Send message to device"
- device received the message and temperature starts decreasing on device (till 0)
- send {"fan" : "off"} to the stop the fan (then temperature increases again..)
13. set a breakpoint inside sample_entry() (sample_azure_iot.c) function to observe the mqtt publish process (send messages to the cloud)
14. set a breakpoint inside my_notify_func() (sample_azure_iot.c) function to observe mqtt message get process (receive messages from the cloud)
15. (....)
