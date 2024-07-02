# Here's the to-do list:
* Using `HACS`, add the `Platinum Weather Card` to your frontend integrations. Be aware it is no longer being maintained.  
* Download the 3 files above and replace all `kxxx` entries with your local NWS observation reporting station code.

  https://www.cnrfc.noaa.gov/metar.php
  
  https://www.faa.gov/air_traffic/weather/asos

  Note: The station code will be assigned by the NWS integration if one isn't provided during setup. Refer to the NWS integration service page under `Settings > Devices and services` to see the resolved station code.

  https://rc.home-assistant.io/integrations/nws

* Add the contents of `NWS_trigger_template.yaml` to your `configuration.yaml` file.
* Add the contents of `weather_modern.yaml` to your HA configuration.  You can add it to `configuration.yaml` or use a split configuration (links below).   If split, ensure you provide any required `!include` directive. 
  
  https://www.home-assistant.io/docs/configuration/splitting_configuration/, and/or https://www.home-assistant.io/docs/configuration/packages/
  
* Navigate to `Developer-tools > YAML` and perform a `CONFIGURATION CHECK`. If good, perform an HA restart, and check the `home-assistant.log` for the absence of errors.
* Confirm the `Platinum Weather Card` integration is running by navigating to `Settings > Dashboards`, clicking on the stacked dots in the upper right corner, and selecting `Resources`.  The `platinum-weather-card.js` file should be listed.
* Navigate to a dashboard and add a `Custom: Platinum Weather Card` to it.  Select `SHOW CODE EDITOR`, delete any existing YAML and replace it with the contents of `platinum_wx_card.yaml`.

## That should do it!


###   Notes:

*	The weather_modern.yaml file, while targeted toward the Platinum Weather Card, may work well for other weather cards.  Its main function is to follow the progression of the NWS forecasts which, at certain times, contain three forecast indexes within the same calendar day.  Except for the current near-term textual forecast, which is always at index [0], templates will deliver only the daytime forecasts for the following 6-7 days.  The same function could be expanded to include nighttime forecasts, which assumes there’s an HA UI card that can accommodate the data.
  
*	The weather_modern.yaml file was assembled using my limited knowledge of Jinja2.  That said, it’s relatively easy to understand and works well.

*	Regarding the Platinum Weather Card as used with the NWS integration, there are two shortfalls that could be addressed by someone having a good understanding of its source code.

    1.	The updates to the NWS forecasts seldom occur at or near the top of each hour.  Currently, the Platinum Weather Card will shift the day-of-the-week legends at midnight.  This will result in a premature shifting of the legends until the NWS midnight forecast arrives.  For NWS, the proper method would be to synchronously tie the shifting of days to the arrival of the midnight forecast.

        There is, however, an additional element relating to correcting the shifting of days.  What occasionally happens is the prior-hour’s NWS forecast reappears within an hour of the latest update.  When this happens after midnight, there should be the ability to revert the legends back to the prior-day forecast.  This should happen naturally if the ordering is strictly a function of datetime[0].

    2.	Per observation, the NWS textual forecasts get more verbose as adverse weather conditions approach a configured location.  Sometimes these are beyond the 255-character limit of an entity state.  A better implementation uses entity attributes, which have a much larger limit.  Thankfully, the NWS integration provides textual forecasts as attributes; however, only the Extended Section Forecast is able to use it.  Unfortunately, the blue pop-up tooltip forecasts can only accommodate entities.  
