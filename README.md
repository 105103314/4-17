# Blynk Python Library
Provides API for [Blynk Server][blynk-server] communication and messaging on IoT/desktop systems with Micropython/Python support. 
__________

### Blynk is **the most popular Internet of Things platform** for connecting hardware to the cloud, designing apps to control them, and managing your deployed devices at scale. 

- With Blynk Library you can connect **over 400 hardware models** (including ESP8266, ESP32, NodeMCU, all Arduinos, Raspberry Pi, Particle, Texas Instruments, etc.)to the Blynk Cloud.
Full list of supported hardware can be found [here][blynk-hw].

- With Blynk apps for **iOS** and **Android** apps you can easily build graphic interfaces for all of your projects by simply dragging and dropping widgets on your smartphone. It's a purely WYSIWG experience: no coding on iOS or Android required. 

- Hardware can connect to Blynk Cloud (open-source server) over the Internet using hardware connectivity on board, or with the use of various shields (Ethernet, WiFi, GSM, LTE, etc). Blynk Cloud is available for every user of Blynk **for free**. 

![Blynk Banner][blynk-banner]


## Installation of Blynk Python Library 

#### Installation via python pip
 - Check python availability in your system. 
   ```commandline
   python --version
   ``` 
   To exclude compatibility issue preferable versions are Python 2.7.9 (or greater) or Python 3.4 (or greater)
   If python not present you can download and install it from [here][python-org]. 
   
   Note! To run python in "sandbox" you can try **virtualenv** module. Examine [this link][virtual-env] how to do it.
      
 - If you’re using preferable versions of python mentioned above, then **pip** comes installed with Python by default. 
   Check pip availability:
   ```commandline
   pip --version
   ```    
 - Install blynk library
   ```commandline
   sudo pip install blynklib
   ``` 

#### Manual installation
Library can be installed locally from git sources: 
   
```commandline 
git clone https://github.com/blynkkk/lib-python.git
cd lib-python
pip install --user -e .

# sudo pip install -e .  # if installation needed not for current but for all users
``` 

#### Testing
You can run unit tests on cPython systems using the command:

    python setup.py test

***Note! Unit Tests for Micropython ENV currently not implemented***

#### Micropython installation
Some hardware platforms can use **[Micropython][micropython-org]** package.
This is helpful for preliminary testing and debugging of your code outside of real hardware. Supported platforms 
and related installation docs can be found [here][micropython-pkg].


## Features
Library allows to communicate with public or local [Blynk Server][blynk-server].
 
Supports Python2/Python3/Micropython.

HW support of RaspberryPi/ESP32

##### List of available operations:
 - subscribe to connect/disconnect events 
 - subscribe to read/write events of [virtual pins][blynk-vpins]
 - [virtual pin][blynk-vpins] write
 - [virtual pin][blynk-vpins] sync
 - send mobile app push notifications
 - send email notifications
 - send twitter notifications
 - change certain widget properties
 

## Quickstart 
Install Blynk python library

Install Blynk App: 
[<img src="https://cdn.rawgit.com/simple-icons/simple-icons/develop/icons/googleplay.svg" width="18" height="18" /> Google Play][blynk-app-android] | 
[<img src="https://cdn.rawgit.com/simple-icons/simple-icons/develop/icons/apple.svg" width="18" height="18" /> App Store][blynk-app-ios]**

- Create new account in Blynk app using your email address
- Create a new Project in Blynk app 
- You will get Auth Token delivered to your email account. 
- Put this Auth Token within your python script to authenticate your device on [public][blynk-server-public] or [local][blynk-server]

```py
BLYNK_AUTH = '<YourAuthToken>' #insert your Auth Token here
```

#### Usage example
```py
import blynklib

BLYNK_AUTH = '<YourAuthToken>' #insert your Auth Token here
# base lib init
blynk = blynklib.Blynk(BLYNK_AUTH) 
# advanced options of lib init
# from __future__ import print_function
# blynk = blynklib.Blynk(BLYNK_AUTH, server='blynk-cloud.com', port=80, heartbeat=10, rcv_buffer=1024, log=print)

# register handler for Virtual Pin V22 reading.
# for example when a widget in Blynk App asks Virtual Pin data from server within given interval    
@blynk.handle_event('read V22')
def read_virtual_pin_handler(pin):
    
    # your code goes here
    # ...
    # Example: get sensor value, perform calculations, etc
    sensor_data = '<YourCalculatedSensorData>'
    critilcal_data_value = '<YourCriticalSensorValue>'
        
    # send value to Virtual Pin and store it in Blynk Cloud 
    blynk.virtual_write(pin, sensor_data) #example: blynk.virtual_write(24, sensor_data)
        
    # you can perform actions if value reaches a threshold (e.g. some critical value)
    if sensor_data >= critilcal_data_value
        
        blynk.set_property(pin, 'color', '#FF0000') # set red color for the widget UI element 
        blynk.notify('Warning critical value') # send push notification to Blynk App 
        blynk.email(<youremail@email.com>, 'Email Subject', 'Email Body') # send email to specified address
        
# main loop that starts program and handles registered events
while True:
    blynk.run()
```
## More Examples

Learn **[more_examples][blynk-py-examples]** to get familiar with basic features usage.

#### Examples List:

##### Core operations:
- 01_write_virtual_pin.py (virtual pin write event handling)
- 02_read_virtual_pin.py  (App read virtual pin events handling)
- 03_connect_disconnect.py (library connect/disconnect events handling)
- 04_email.py(send email support)               
- 05_set_property_notify.py (changing App widget properties and send internal notifications)
- 06_terminal_widget.py (App communication with device through terminal widget)
- 07_tweet_and_logging.py (Tweet messaging and library logging options)

##### Raspberry Pi (any):
- 01_weather_station_pi3b.py (DHT22; BMP180 sensors usage)

##### ESP32
- 01_touch_button.py (TTP223B sensors usage)



### License
This project is released under The MIT License (MIT)


  [lib-release]: https://github.com/blynkkk/lib-python/releases/latest
  [lib-licence]: https://github.com/blynkkk/lib-python/blob/master/LICENSE
  [lib-travis]: https://travis-ci.org/blynkkk/lib-python
  [lib-issues]: https://github.com/blynkkk/lib-python/issues
  [lib-stars]: https://github.com/blynkkk/lib-python/stargazers
  [lib-network]: https://github.com/blynkkk/lib-python/network
  [blynk-io]: https://github.com/blynkkk/blynkkk.github.io
  [blynk-hw]: https://github.com/blynkkk/blynkkk.github.io/blob/master/SupportedHardware.md
  [blynk-architecture]: https://github.com/blynkkk/blynkkk.github.io/blob/master/images/architecture.png
  [blynk-banner]: https://github.com/blynkkk/blynkkk.github.io/blob/master/images/GithubBanner.jpg
  [blynk-server]: https://github.com/blynkkk/blynk-server
  [blynk-server-public]: http://blynk-cloud.com
  [blynk-docs]: https://docs.blynk.cc/
  [blynk-py-examples]: https://github.com/blynkkk/lib-python/blob/master/examples
  [blynk-app-android]: https://play.google.com/store/apps/details?id=cc.blynk
  [blynk-app-ios]: https://itunes.apple.com/us/app/blynk-control-arduino-raspberry/id808760481?ls=1&mt=8
  [blynk-vpins]: http://help.blynk.cc/getting-started-library-auth-token-code-examples/blynk-basics/what-is-virtual-pins
  [python-org]: https://www.python.org/downloads/
  [micropython-org]: https://micropython.org/ 
  [micropython-pkg]: https://github.com/micropython/micropython/wiki/Getting-Started
  [virtual-env]: https://virtualenv.pypa.io/en/latest/installation/
