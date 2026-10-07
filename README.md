## AndroidAutoStub

- stock AndroidAutoStub extracted from [NikGapps](https://nikgapps.com/)
- custom built Google Search App and Google Speech Services Stubs


## Build with [docker-lineage-cicd](https://github.com/lineageos4microg/docker-lineage-cicd)
This was build and tested on LineageOS for microG 23.2 (build target bramble) on a Pixel 4a 5G.

Add this to your manifests:
```
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
          <project name="TheSmolBoi/android-auto-stub" path="prebuilts/androidauto" remote="github" revision="main" />
</manifest>
```

Add these three apps to your CUSTOM_PACKAGES environment variable:
```
CUSTOM_PACKAGES: AndroidAuto gappsstub speechservicestub
```

Add this to your ```before.sh``` in your userscripts directory:
```
#!/bin/bash
set -euo pipefail

OVERLAY_DIR="vendor/lineage/overlay/microg/frameworks/base/core/res/res/values"
mkdir -p "$OVERLAY_DIR"
cat > "$OVERLAY_DIR/config_androidauto.xml" <<'XML'
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <!-- The names of the packages that will hold the automotive projection role. -->
    <string name="config_systemAutomotiveProjection" translatable="false">com.google.android.projection.gearhead</string>
</resources>
XML
echo ">> [$(date)] [aa] wrote $OVERLAY_DIR/config_androidauto.xml"
```

Build your custom ROM (microG is required)


## Get android auto setup

- Install the latest android auto apk (you can find this online or get it with aurora store)
- Install google maps in the same way
- open google maps once, grant it location permissions. Just while in use is fine.
- android auto *should* just work now

if you get stuck on google maps permission, try pressing cancel instead of settings.

if you are having trouble with first time setup, I found it was helpful to setup the bluetooth connection to the car before plugging in the usb c.


## Sources

sources for custom built stubs with build instructions for each of the stubs:
- [speechservicesstub](https://github.com/SolidEva/SpeechServices-Package-Spoof)
- [gappsstub](https://github.com/SolidEva/Gapp-Package-Spoof)

## Thanks
big thanks to @dylangerdaly and the thread [here](https://github.com/microg/GmsCore/issues/897)

