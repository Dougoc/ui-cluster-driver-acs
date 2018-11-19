# ui-plugable-cluster-driver
Skeleton Rancher UI driver for custom Kubernetes cluster drivers

NOTE: This is a working example of a plugable cluster driver which uses [this driver](https://github.com/rancher/kontainer-engine-example-driver/releases/download/v0.1.0/kontainer-engine-example-driver-linux) as its cluster driver.
This is a port of the built-in Google GKE driver and simply exists as an example of how to build your own cluster driver. Do not use in production.

## Setup

* Fork this repository into your own account as `ui-cluster-driver-DRIVERNAME`
  * DRIVERNAME should be the name of the driver that you would give to `TBD`, e.g. "mycompany", "digitalocean", etc.
* Update the "name" in package.json to match
  * You should also update description, URLs, etc, but these aren't strictly required.
* `npm install`

## Development

This package contains a small web-server that will serve up the custom driver UI at `http://localhost:3000/component.js`.  You can run this while developing and point the Rancher settings there.
* `npm start`
* The driver name can be optionally overridden: `npm start -- --name=DRIVERNAME`
* The compiled files are viewable at http://localhost:3000.
* Do not use the `model.<drivername>EngineConfg` signature to access your driver config in the template file, use the `config` alias that is already setup in the component

## Building

For other users to see your driver, you need to build it and host the output on a server accessible from their browsers.

* `npm run build`
* Copy the contents of the `dist` directory onto a webserver.
  * If your Rancher is configured to use HA or SSL, the server must also be available via HTTPS.

## Using

* Add a Cluster Driver in Rancher 2.0 (Global -> Custom Drivers -> Cluster Drivers)
  * Name: Your `DRIVERNAME` (see above).
  * Download URL: The URL for the driver binary (e.g. `https://github.com/mycompany/kontainer-engine-mycompany/releases/download/v1.0.0/kontainer-engine-driver-mycompany-v1.0.0-linux-amd64.tar.gz`)
  * Custom UI URL: The URL you uploaded the `dist` folder to, e.g. `https://github.com/mycompany/ui-cluster-driver-mycompany/releases/download/v1.0.0/component.js`)
* Wait for the driver to become "Active"
* Go to Clusters -> Add Cluster, your driver and custom UI should show up.
