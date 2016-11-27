# OnePlayerCore_GettingStarted

## Focus : 

The links to the player will be provided to you by Akamai (CDN) as below :

    $ http://hss-live-c1-aka.canal-plus.com/player/prod/playerCore/one-player-core.js
    $ http://hss-live-c1-aka.canal-plus.com/player/prod/playerCore/one-player-core.min.js

for more details about implementation of our player please *[see there](https://github.com/canalplus/one-player-core/blob/master/README.md)*
or check our *[repo](https://github.com/canalplus/one-player-core/blob/)*


if you don't have right try this [one](https://github.com/canalplus/rx-player) `Rx-player` which is our Open source version.

    
  
## Sample

in a video tag you just have to set an identifier and launch one-player-core on it :

        <video id="videoEl" controls></video>

to launch one-player-core , you must 

        var player = new RxPlayer({
          videoElement: document.getElementById("videoEl"),
        });

You must set some parameters like : 

```
var keySystems = [
      {
        type: "widevine",
        getLicense: function getLicense(challenge) {
          return request({
            method: "POST",
            url: "https://vod-authorization.canal-overseas.com/vod/play/wvX1?eck=X1",
            data: btoa(bytesToStr(challenge)),
            headers: {
              mediaPackId: "subscription-c-ald",
              optionId: "streaming",
              productId: "1186603_1"
            },
            format: "json",
          })
          .map(function (response) {
            return strToBytes(atob(response.licence));
          });
        }
      }
  ]

player.loadVideo(
  {
  "url": "http://hss-vod-aka.canal-overseas.com/vod/assets/subscription-c-ald_1186603_1/_/hss-wv-cp-drom-hd/Manifest",
  "transport": "smooth",
  "keySystems": keySystems,
  "live": true,
})

player.play();

```

The `requests` function is a custom implementation, look the sample file for more detail.

 
## Run it : 
 You must have a client certificat or use a X1 ( cube C ) to get licence by our DRM platform.
 
