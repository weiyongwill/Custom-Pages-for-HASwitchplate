# Custom-Pages-for-HASwitchplate
Custom pages for [HASwitchplate](https://github.com/aderusha/HASwitchPlate) created by @aderusha

Features
====
* Two themes to choose from
* Access Weather/Time, Toggles and Media Player via NavBar Buttons
* Menu Page to access:
  - Thermostat
  - Sliders
  - 3D Printer
  - Scripts
* Playlists for Media Player:
  - Access by pressing Media Player NavBar Button while on the Media Player page
* Two pages for toggles by pressing the toggles page button

Changelog
====
#### Update 0.4
- Add shell script for faster first time setup
- Add automation to switch back to the Clock/Weather Page, if there is no button press for 20 seconds.

#### UPDATE 0.33
- Fix automation trigger on page change for p5, p6, p7, p9

#### UPDATE 0.32
- **Major: Add Thermostat Page**:
  To use the thermostat add ```hasp_plate01_p5_thermostat.yaml``` to your HASP folder and replace the entities with your thermostat.
- **Migrate all pages to standard theme**
- **Pressing a button that changes pages now is coded in the Nextion Firmware.** This change makes going through pages more responsive. If you're coming from an earlier release turn off every automation that switches pages or delete them in the YAML files. Or replace ```hasp_plate01_p0_pages.yaml```
  You need to flash the new firmware for the Nextion panel. 
  Add ```hasp_plate01_p5_thermostat.yaml``` to your config and replace every ```climate.DUMMY``` in the file with your thermostat component.

  ![alt text](https://raw.githubusercontent.com/zonko16/Custom-Pages-for-HASwitchplate/beta/Thermostat.png)
     
#### UPDATE 0.3
- **Alternative Theme** available.
  Replace the firmware with the new one according to your panel. Nothing else has to be changed. The firmwares with the new theme end with ```_alternate_theme_*.yaml```.

- New Pages added
  There is a set of new Pages added to HASP.
  Pressing button 1 (Hamburger Icon) on the Date/Weather page will open up a menu where you can access further functions
  The extended funcionalty will only work with the alternate theme for now. Follow Instructions to get the new Pages working

  ![alt text](https://raw.githubusercontent.com/zonko16/Custom-Pages-for-HASwitchplate/beta/Menu.png)

#### UPDATE 0.2:  
- Your now able to switch between two pages on Page 6 (Toggles) by pressing the toggles button in the Navigation Bar again.
- Simplified setting up entities for Page6 (Toggles). See Step 4 in Quick start.

Preview
===
**Standard Theme**
![alt text](https://raw.githubusercontent.com/zonko16/Custom-Pages-for-HASwitchplate/master/Preview.png)

**Alternative Theme**

![alt text](https://raw.githubusercontent.com/zonko16/Custom-Pages-for-HASwitchplate/beta/preview_alternate_theme.png)


QUICK START
=====

1. Flash the ESP8266 and the Nextion panel as usual but use one of these [Nextion Firmwares according to your panel size, orientation and theme you want to use](https://github.com/zonko16/Custom-Pages-for-HASwitchplate/tree/master/Nextion_Firmware), provided by this repository instead. 

2. (a)You can run a script for an easier/faster setup.
You will need to SSH to run the script.
**Hass.IO users running the SSH Addon:**
Open the terminal and execute:

```
cd /config
apk add tar wget
bash <(wget -qO- -o /dev/null https://github.com/zonko16/Custom-Pages-for-HASwitchplate/raw/master/deploy_script/deploy.sh)
```

**Standard Home Assistant users:**
```
sudo su -s /bin/bash homeassistant
cd ~/.homeassistant
bash <(wget -qO- -o /dev/null https://github.com/zonko16/Custom-Pages-for-HASwitchplate/raw/master/deploy_script/deploy.sh)
```

You can skip the rest of the installation guide if you ran through the script.

2.(b) Replace the yaml files in ```config/packages/plate01``` with the ones provided in this repository.
    - For the **2.4" Panel** use .yamls in [packages_2.4in/](https://github.com/zonko16/Custom-Pages-for-HASwitchplate/tree/master/packages_2.4in) 
    - For the **3.2" Panel** use .yamls in [packages_3.2in/](https://github.com/zonko16/Custom-Pages-for-HASwitchplate/tree/master/packages_3.2in)

  **Update 0.3:** Access a Menu with extra pages.
  Coming from previous release add/replace ```hasp_plate01_p0_pages.yaml```, ```hasp_plate01_p1_menu.yaml```, ```hasp_palte01_p2_scripts.yaml```, ```hasp_plate01_p4_sliders.yaml```, ```hasp_plate01_p7_playlist.yaml```
  It's recommended to deactivate any colorconfig.yaml as colors are already set in the firmware.

3. Replace YOUR_API_KEY in ```hasp_plate01_00_components.yaml``` your own Darksky API 

4. Replace the entities and names to your liking for every page in the different YAML files.
Entities that need to be changed are called like **switch.YOUR_ENTITY**, **senor.YOUR_TEMPERATURE** and so on.
**IMPORTANT UPDATE:** This step hast been considerably simplified for page 6. 
- Open ```hasp_plate01_p6_entities.yaml```
- In there you'll find 
```
hasp_plate01_p6_toggle1-12(16):
  name: Toggle 1-12(16)
  entities:
  - switch.DUMMY
```
- replace **switch.DUMMY** with the component you are using for ever single button and set the name for your toggle.

5. (3.2" users skip this step) If you're using a **second temperature/humidity** and want to switch between In and  Out by clicking on the displayed temperature uncomment lines 16 to 23 in ```hasp_plate01_p3_weather.yaml```
(Coming from previous releases these lines were in ```hasp_plate01_p0_components.yaml``` if switching temperature doesn't work copy below lines into ```hasp_plate01_p3_weather.yaml```):

```
####################################################################
# Toggles the Label and Temp/Humidity displayed on Page 3. Thanks @madrian
#  - alias: hasp_plate01_p0_ChangeToTempInOut
#    trigger:
#    - platform: mqtt
#      topic: 'hasp/plate01/state/p[3].b[6]'
#      payload: 'ON' 
#    action:
#    - service: input_boolean.toggle
#      entity_id: input_boolean.hasp_plate01_p3_temperatureswitch
```




**_Page 3 Weather Setup_**

You'll need a [Darksky API](https://darksky.net/dev) to use the weather component. Place your API key into ```hasp_plate01_p3_weather.yaml```. 

Special thanks to **@aderusha** for creating HASwitchPlate and **@madrian** for spending hours of beta testing with me. 



