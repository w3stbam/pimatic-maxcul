pimatic-maxcul
=======================

Pimatic plugin to control MAX! home heating devices with a Busware CUL868 usb wireless stick.

At the moment the software is at a development stage so please use it with caution.

More informations and function will be coming soon.

WORK IN PROGRESS

Usage
---------
The maxcul Plugin automatically detects incoming pairing messages and reacts accordingly.
If you start pimatic with the plugin enable you can enable the debug mode in the settings to get the deviceIds extracted from the incomming pairing messages.

Example Plugin Configuration

    {
      "plugin": "maxcul",
      "serialPortName": "/dev/ttyACM0",
      "homebaseAddress": "123456",
      "enablePairMode": false,
      "baudrate": 9600
    }

Example device Configuration shutter contact

    {
      "id": "shutter-1",
      "class": "MaxculShutterContact",
      "name": "Shutter Contact 1",
      "deviceId": "020BFF"
    }

Example device Configuration heating thermostat

    {
      "id": "heatingthermostat-01",
      "class": "MaxculHeatingThermostat",
      "name": "Thermostat 1",
      "deviceId": "0D0CF6",
      "groupId": "00",
      "guiShowModeControl": true,
      "guiShowPresetControl": true,
      "guiShowTemperatureInput": true,
      "guiShowMeasuredTemperature": true,
      "guiShowBatteryState": true,
      "guiShowConfigButton": true,
      "ecoTemp": 17,
      "comfyTemp": 20,
      "minimumTemperature": 4.5,
      "maximumTemperature": 30.5,
      "measurementOffset": 0,
      "windowOpenTime": 60,
      "windowOpenTemperature": 4.5
    },

Changelog
---------------

* v0.1.0

    This first Version enables the user to receive messages from the MAX! devices. It receives the
messages, decodes them and prints them to the console or log as debuging information.

* v0.2.0

    This version enables you to pare the max shutter contacts with the pimatic system and use them as
sensor. Also you can pair the heating thermostats so that they can get the time informations from the
pimatic system an set the mode (auto/boost/manuel) and switch between the comfy and eco temperature.

* v0.2.5

    This Version enables the user to use the thermostat heating elements. You can now set the desired temperature, the mode, show the battery state and the measured temperature in the pimatic frontend

* v0.2.9

    Now you can disable or enable the pair feature. So you can lock your system against foreign devices

* v0.3.0

    There is now an "off"-Button so that we can set the heating thermostat to off with one click. Also there is now a better input checking for the temperature input with an info message if the input is out of range. The input must be between 4.5 (off) and 30.5 (full on).

* v0.3.1

    Fixed a bug witch prevents the shutter contacts from updating.

* v0.4.0

    You can now define some default values for each heating thermostat that can be written wirelessly to the device itself. So you can set a min and max temperature in the device.If this is set, a user can only set a value between this value if he is setting the temperature physically on the device itself. You can set this value in the device config and enable a transmit button in the frontend.If this is clicked the data where transfered to the device. Also this version fixed a bug witch sets the shutter contact to a wrong value.

* v0.4.1

    Fixed a wrong type for an initial variable value

* v0.5.0

    Added rewritten communication layer with retransmit, timeout and promise support for a better reliability. Also cleaned up the code.
    Disabled the "auto" mode button, because there is no support to config this mode at the moment.

* v0.5.1

    Added Missing Class file.

* v0.5.2

    Removed the HiPack dependency, this npm package is no longer developed and so we need to remove it for the further development of the pimatic 0.9 compatibility.
    We also changed the serial port timeouts and logging levels for a better user experience

ToDo
-------
* CUL Credit System support to respect the ISM Band 1% Rules
* Add group support to handle groups of devices as one
* Monitoring Mode to receive only the messages without responding
* Support for programming Week Profile (at the moment there is only the default program in "Auto Mode")
* possibility to pair the shutters an heating elements directly
* additional error handling
* Wall-Thermostat support
* Push Button support
* Implement ConfigValve support to configure the boost duration
* pimatic 0.9 support
