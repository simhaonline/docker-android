Docker-Android
==============

[![Build Status](https://travis-ci.org/butomo1989/docker-android.svg?branch=master)](https://travis-ci.org/butomo1989/docker-android)
[![codecov](https://codecov.io/gh/butomo1989/docker-android/branch/master/graph/badge.svg)](https://codecov.io/gh/butomo1989/docker-android)

Android in docker solution with noVNC supported

Requirements
------------

Docker is installed in your system.

Purpose
-------

1. Build android project / application and run unit test
2. Run UI Test for mobile website with appium framework
3. Run UI Test for mobile application with different frameworks (appium, espresso, etc.)
4. Simulate Short Message Service (SMS)

Features
--------

1. Android emulator with different devices
2. latest build-tool (version 25.0.2)
3. noVNC to see what happen inside docker container
4. Appium server for automation test framework and it is able to connect with selenium grid

List of Docker images
---------------------

|Supported OS   |Android version   |API level   |Image name   |Image status   |
|:---|:---|:---|:---|:---:|
|Linux|5.0.1|21|butomo1989/docker-android-x86-5.0.1|[![](https://images.microbadger.com/badges/image/butomo1989/docker-android-x86-5.0.1.svg)](https://microbadger.com/images/butomo1989/docker-android-x86-5.0.1 "Get your own image badge on microbadger.com")|
|Linux|5.1.1|22|butomo1989/docker-android-x86-5.1.1|[![](https://images.microbadger.com/badges/image/butomo1989/docker-android-x86-5.1.1.svg)](https://microbadger.com/images/butomo1989/docker-android-x86-5.1.1 "Get your own image badge on microbadger.com")|
|Linux|6.0|23|butomo1989/docker-android-x86-6.0|[![](https://images.microbadger.com/badges/image/butomo1989/docker-android-x86-6.0.svg)](https://microbadger.com/images/butomo1989/docker-android-x86-6.0 "Get your own image badge on microbadger.com")|
|Linux|7.0|24|butomo1989/docker-android-x86-7.0|[![](https://images.microbadger.com/badges/image/butomo1989/docker-android-x86-7.0.svg)](https://microbadger.com/images/butomo1989/docker-android-x86-7.0 "Get your own image badge on microbadger.com")|
|Linux|7.1.1|25|butomo1989/docker-android-x86-7.1.1|[![](https://images.microbadger.com/badges/image/butomo1989/docker-android-x86-7.1.1.svg)](https://microbadger.com/images/butomo1989/docker-android-x86-7.1.1 "Get your own image badge on microbadger.com")|
|OSX / Windows|5.0.1|21|butomo1989/docker-android-arm-5.0.1|[![](https://images.microbadger.com/badges/image/butomo1989/docker-android-arm-5.0.1.svg)](https://microbadger.com/images/butomo1989/docker-android-arm-5.0.1 "Get your own image badge on microbadger.com")|
|OSX / Windows|5.1.1|22|butomo1989/docker-android-arm-5.1.1|[![](https://images.microbadger.com/badges/image/butomo1989/docker-android-arm-5.1.1.svg)](https://microbadger.com/images/butomo1989/docker-android-arm-5.1.1 "Get your own image badge on microbadger.com")|
|OSX / Windows|6.0|23|butomo1989/docker-android-arm-6.0|[![](https://images.microbadger.com/badges/image/butomo1989/docker-android-arm-6.0.svg)](https://microbadger.com/images/butomo1989/docker-android-arm-6.0 "Get your own image badge on microbadger.com")|
|OSX / Windows|7.0|24|butomo1989/docker-android-arm-7.0|[![](https://images.microbadger.com/badges/image/butomo1989/docker-android-arm-7.0.svg)](https://microbadger.com/images/butomo1989/docker-android-arm-7.0 "Get your own image badge on microbadger.com")|
|OSX / Windows|7.1.1|25|butomo1989/docker-android-arm-7.1.1|[![](https://images.microbadger.com/badges/image/butomo1989/docker-android-arm-7.1.1.svg)](https://microbadger.com/images/butomo1989/docker-android-arm-7.1.1 "Get your own image badge on microbadger.com")|

Quick Start
-----------

1. Enable **Virtualization** under **System Setup** in **BIOS**. (It is only for Ubuntu OS. If you use different OS, you can skip this step).

2. Run docker-android

	```bash
	docker run --privileged -d -p 6080:6080 -p 4723:4723 -p 5554:5554 -p 5555:5555 -e DEVICE="Samsung Galaxy S6" --name android-container butomo1989/docker-android-x86-5.0.1
	```

	**Optional arguments**

		-v <android_project_or_apk>:/root/tmp	: You need to share volume or apk file if for example you want to build the android project inside docker container or you want to run UI test by using appium.
		-e APPIUM=True: If you want to use appium as UI test framework to test mobile website or android application

3. Verify the ip address of docker-machine.

   - For OSX, you can find out by using following command:

     ```bash
     docker-machine ip default
     ```

   - For different OS, localhost should work.

4. Open ***http://docker-machine-ip-address:6080*** from web browser.

   ![][noVNC]


Connect to Selenium Grid
------------------------

This feature can be used only if you set **APPIUM=True** in environment variable.

**Arguments**

	-e CONNECT_TO_GRID=True	: to connect appium server to your selenium grid.
	-e APPIUM_HOST="<host_ip_address>": where / on which instance appium server is running. Default value: 127.0.0.1
    -e APPIUM_PORT=<port_number>: which port appium server is running. Default port: 4723
    -e SELENIUM_HOST="<host_ip_address>": where / on which instance selenium grid is running. Default value: 172.17.0.1
    -e SELENIUM_PORT=<port_number>: which port selenium grid is running. default port: 4444

![][connect to grid 1]  ![][connect to grid 2]

List of Devices
---------------

Type | Device Name
--- | ---
Phone | Samsung Galaxy S6
Phone | Nexus 4
Phone | Nexus 5
Phone | Nexus 5x
Phone | Nexus 6
Phone | Nexus 6P
Phone | Nexus One
Phone | Nexus S
Tablet | Pixel C
Tablet | Nexus 7
Tablet | Nexus 9
Tablet | Nexus 10

![][galaxy s6] ![][nexus 5]

Control android emulator outside container
------------------------------------------

```bash
adb connect <docker-machine-ip-address>:5555
```

![][adb_connection]

**Note:** You need to have Android Debug Bridge (adb) installed in your host machine.

SMS Simulation
--------------

1. Using telnet
	- Find the auth_token and copy it.

	 ```bash
	 docker exec -it android-container cat /root/.emulator_console_auth_token
	 ```

	- Access emulator using telnet and login with auth_token

	 ```bash
	 telnet <docker-machine-ip-address> 5554
	 ```

	- Login with given auth_token from 1.step

	 ```bash
	 auth <auth_token>
	 ```

	- Send the sms

	 ```bash
	 sms send <phone_number> <message>
	 ```

2. Using adb

	 ```bash
	 docker exec -it android-container adb emu sms send <phone_number> <message>
	 ```

3. You can also integrate it inside project using [adblib].

![][sms]

Troubleshooting
---------------
All logs inside container are stored under folder **/var/log/supervisor**. you can print out log file by using **docker exec**. Example:

```bash
docker exec -it android-container tail -f /var/log/supervisor/docker-appium.stdout.log
```

[noVNC]: <images/noVNC.png> "login with noVNC to see what happen inside container"
[connect to grid 1]: <images/appium_with_selenium_grid_01.png>
[connect to grid 2]: <images/appium_with_selenium_grid_02.png>
[galaxy s6]: <images/run_under_galaxy_s6.png>
[nexus 5]: <images/run_under_nexus_5.png>
[adb_connection]: <images/adb_connection.png>
[sms]: <images/SMS.png>
[adblib]: <https://github.com/tananaev/adblib>
