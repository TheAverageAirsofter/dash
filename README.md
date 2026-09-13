# Dash

Live telemetry and register tuning for Fardriver motor controllers, as an
installable web app. Works on Android. Bluetooth does not work on iPhone —
see the bottom of this file.

## Files

| File | What it is |
|---|---|
| `index.html` | The riding dashboard |
| `tuner.html` | The register workbench |
| `manifest.webmanifest` | Makes it installable |
| `sw.js` | Caches the app so it opens without signal |
| `icon-*.png` | Home screen icons |

All seven files must sit in the same folder.

## Putting it online

Bluetooth only works over HTTPS. Opening the file from your Downloads folder
will show the interface but the Connect button will fail. Hosting is required,
and GitHub Pages is free.

1. Make a GitHub account.
2. Click **New repository**, name it `dash`, tick **Public**, create it.
3. On the repo page click **uploading an existing file**, drag in all seven
   files, click **Commit changes**.
4. Go to **Settings → Pages**. Under Branch pick `main`, folder `/ (root)`,
   click **Save**.
5. Wait about a minute, then reload. The page shows your URL — something like
   `https://yourname.github.io/dash/`.

## Installing it on the phone

Open that URL in **Chrome** on Android. Menu (three dots) → **Add to Home
screen** → **Install**.

You now have an icon in the app drawer. Opening it gives you a fullscreen app
with no address bar. Android treats it as a real app in the recents list.

## Updating it

Edit the file, upload it to GitHub, and **change the `VERSION` string at the
top of `sw.js`** — otherwise phones keep serving the cached copy and your
change never appears. Any new value works: `dash-v2`, `dash-v3`.

## Before you ride with it

Check the Packet inspector on the dashboard. Hex lines with green address tags
mean your controller is talking. Red `crc` tags mean the checksum differs on
your firmware. Nothing at all means the characteristic UUID is different —
use nRF Connect to find the one marked NOTIFY on your dongle, then add it to
the `CHARS` list near the top of the script in both files.

Set pole pairs and wheel circumference under **Bike setup** before trusting the
speed reading.

## Writes

The tuner can write to the controller. It stays locked until you unlock it,
refuses values outside limits you set, and reads every write back to confirm
it landed. None of that protects you from writing a correct value to the wrong
register. Wheel off the ground, nobody on the bike, until you trust your map.

## Why there is no iPhone version

Safari has no Web Bluetooth and Apple does not allow other browser engines to
add it. An iPhone version needs a native app built with Capacitor or Flutter,
a Mac, and a $99/year Apple Developer account.

## If you want a real APK later

Reasons to bother: Play Store listing, background ride logging with the screen
off, and users who never figure out "Add to Home screen". Capacitor wraps these
same files — nothing here gets thrown away.
