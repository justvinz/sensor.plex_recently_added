___

<h1 align="center"> :warning:  THIS IS THE DEV BRANCH!  :warning:</h1>
<h2 align="center">
May contain bugs, broken features, and should generally be avoided.</br></br>

___


# Plex Recently Added Component

Home Assistant component to feed [Upcoming Media Card](https://github.com/custom-cards/upcoming-media-card) with
Plex's recently added media.</br>
This component does not require, nor conflict with, the default Plex components.</br></br>
<link href="https://fonts.googleapis.com/css?family=Lato&subset=latin,latin-ext" rel="stylesheet"><a class="bmc-button" target="_blank" href="https://www.buymeacoffee.com/FgwNR2l"><img src="https://www.buymeacoffee.com/assets/img/BMC-btn-logo.svg" alt="Buy me a coffee"><span style="margin-left:5px">If you feel I deserve it, you can buy me a coffee</span></a></br>
</br>

## Installation:

1. Install this component by copying to your `/custom_components/sensor/` folder.
2. Install the card: [Upcoming Media Card](https://github.com/custom-cards/upcoming-media-card)
2. Add the code to your `configuration.yaml` using the config options below.
3. Add the code for the card to your `ui-lovelace.yaml`. 
3. **You will need to restart after installation for the component to start working.**

### Options

| key | default | required | description
| --- | --- | --- | ---
| token | | yes | Your Plex token [(Find your Plex token)](https://support.plex.tv/articles/204059436-finding-an-authentication-token-x-plex-token/)
| host | localhost | no | The host Plex is running on.
| port | 32400 | no | The port Plex is running on.
| ssl | false | no | Set to true if you use SSL to access Plex.
| max | 5 | no | Max number of items to show in sensor.
| remote_images | true | no | If you don't access Home Assistant remotely or if the Plex server is "public", setting this to false will turn off downloading of images. More info below.
| ssl_cert | false | no | If you provide your own SSL certificate in Plex's network settings set this to true.

#### By default this addon automatically downloads images from Plex to your /www/custom-lovelace/upcoming-media-card/ directory. The directory is automatically created & only images reported in upcoming list are downloaded. Images are small in size and are removed automatically when no longer in the upcoming list. This is required to view the images remotely if your Plex server is on your private network.

#### If you don't access Home Assistant remotely (or if the Plex server is "public") you may set remote_images to false, but you either have to set "Secure connections" to "preferred" in your Plex server's network settings or the plex server must provide it's own certificate. This is because the default SSL certificate supplied by Plex is for their own domain and not for your Plex server. If the server provides it's own certificate you only need to set ssl_cert and ssl to true in config.

### Sample for configuration.yaml:

    sensor:
    - platform: plex_recently_added
      token: YOUR_PLEX_TOKEN
      host: 192.168.1.4
      port: 32400
      ssl: true
      max: 10

### Sample for ui-lovelace.yaml:

    - type: custom:upcoming-media-card
      entity: sensor.plex_recently_added


### Card Content Defaults

| key | default | example |
| --- | --- | --- |
| title | $title | "Night of the Living Dead" |
| line1 | $release | "In Theaters Mon, 10/31" if it's a theater release and more than a week away or "Available Monday" if it's a physical release and within a week.|
| line2 | $genres | "Action, Adventure, Comedy" |
| line3 | $rating - $runtime | "★ 9.8 - 01:30"
| line4 | $studio | "Laurel Group Inc."
| icon | mdi:arrow-down-bold | https://materialdesignicons.com/icon/arrow-down-bold

