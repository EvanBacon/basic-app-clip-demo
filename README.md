# App Clip example

- Uses apple-targets to setup App Clip: https://github.com/EvanBacon/expo-apple-targets

Recreate:

- `bunx create-expo my-app`
- `cd my-app`
- `bunx create-target clip`

Issues:

- Need to run `bunx expo prebuild -p ios`, open the project in Xcode, and open the signing tab to ensure signing for the App Clip bundle ID is registered before running `eas build`.
- The version number and build number for the App Clip target must be manually kept in sync with the main app target in Xcode. This doesn't seem supported at the moment.

The codesigning part requires extra requests:

```
curl 'https://developerservices2.apple.com/services/v1/bundleIds' \
-X POST \
-H 'Content-Type: application/vnd.api+json' \
--data-raw '{"data":{"relationships":{"bundleIdCapabilities":{"data":[{"type":"bundleIdCapabilities","attributes":{"enabled":true,"settings":[]},"relationships":{"capability":{"data":{"type":"capabilities","id":"ON_DEMAND_INSTALL_CAPABLE"}},"parentBundleId":{"data":{"type":"bundleIds","id":"XXCCK4F8XX"}}}}]}},"attributes":{"hasExclusiveManagedCapabilities":false,"name":"XC com bacon basic-app-clip-demo clip","teamId":"XX57RJ5UXX","seedId":"XX57RJ5UXX","identifier":"com.bacon.basic-app-clip-demo.clip","bundleType":"onDemandInstallCapable"},"type":"bundleIds"}}'
```
