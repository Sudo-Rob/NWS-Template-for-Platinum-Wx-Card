# Here's the to-do list:
* Using `HACS`, add the `Platinum Weather Card` to your front-end integrations. Be aware it is no longer being maintained.  
* Replace all `kxxx` entries in the 3 files provided herein with your local NWS observation reporting station code.

  https://www.cnrfc.noaa.gov/metar.php
  
  https://www.faa.gov/air_traffic/weather/asos

  Note: The station code will be assigned by the NWS integration if one isn't provided during setup. Refer to the NWS integration service page under `Settings > Devices and services` to see the resolved station code.

  https://rc.home-assistant.io/integrations/nws

* Add the contents of `NWS_trigger_template.yaml` to your `configuration.yaml` file.
* Add the contents of `weather_modern.yaml` to your HA configuration.  You can add it to `configuration.yaml` or use a split configuration (links below).   If split, ensure you provide any required `!include` directive. 
  
  https://www.home-assistant.io/docs/configuration/splitting_configuration/, and/or https://www.home-assistant.io/docs/configuration/packages/
  
* Navigate to `Developer-tools > YAML` and perform a `CONFIGURATION CHECK`. If good, perform an HA restart, and check the `home-assistant.log` for the absensce of errors.
* Confirm the `Platinum Weather Card` integration is running by navigating to `Settings > Dashboards`, clicking on the stacked dots in the uppper right corner, and selecting `Resources`.  The `platinum-weather-card.js` file should be listed.
* Navigate to a dashboard and add a `Custom: Platinum Weather Card` to it.  Select `SHOW CODE EDITOR`, delete any existing YAML and replace it with the contents of `platinum_wx_card.yaml`.

## That should do it!
