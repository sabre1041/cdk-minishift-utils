# Satellite Registration Add-on

This add-on registers minishift using subscriptions from [Red Hat Satellite](https://www.redhat.com/en/technologies/management/satellite) instead of the [Red Hat Network (RHN)](https://rhn.redhat.com/).

<!-- MarkdownTOC -->

- [Using the Satellite Registration Add-on](#using-the-satellite-registration-add-on)
	- [Add-on Variables](#add-on-variables)
	- [Install add-on](#install-add-on)
	- [Start Minishift](#start-minishift)
	- [Apply add-on](#apply-add-on)
	- [Remove add-on](#remove-add-on)
	- [Uninstall add-on](#uninstall-add-on)

<!-- /MarkdownTOC -->

<a name="using-the-satellite-registration-add-on"></a>
## Using the Satellite Registration Add-on

The best way of using this add-on is via the [`minishift addons apply`](https://docs.openshift.org/latest/minishift/command-ref/minishift_addons_apply.html) command which is outlined in the following paragraphs.

<a name="add-on-variables"></a>
### Addon Variables

This add-on requires variables be defined in order to locate the satellite server along with the subscription to apply to the machine.

|Name|Description|
|----|-----------|
|`SATELLITE_CA_URL`|Location of the CA associated with the Satellite server|
|`SATELLITE_ORG`|Organization containing the subscription to apply to the machine|
|`SATELLITE_ACTIVATION_KEY`|Activation key containing the subscription to apply to the machine|

Variables can be specified by adding `--addon-env <key=value>` when the addon is being invoked (either by `minishift start` or `minishift addons apply`).

<a name="install-add-on"></a>
### Install Add-on

Clone this repository onto your local machine and then install the add-on via:

```
    $ minishift addons install <path_to_directory_containing_this_readme>
```

To have minishift apply the add-on during startup, enable the add-on as shown below:

```
    $ minishift addons enable satellite-registration
```

<a name="start-minishift"></a>
### Start Minishift

By default, minishift attempts to subscribe the machine to the Red Hat Network. Since this add-on will replace this functionality, start minishift without registering the machine using the `--skip-registration` flag:

    $ minishift start --skip-registration

Additional flags may also be provided to further customize the runtime. 

<a name="apply-add-on"></a>
### Apply add-on
If Minishift is already started and satellite registration addon is installed. It is possible to register the machine without restarting Minishift (assuming the machine was not previously registered to RHN):

    $ minishift addons apply satellite-registration --addon-env "SATELLITE_CA_URL=<CA_LOCATION>" --addon-env "SATELLITE_ORG=<ORG_NAME>" --addon-env "SATELLITE_ACTIVATION_KEY=<ACTIVATION_KEY>"

<a name="remove-add-on"></a>
### Remove add-on
To unregister the machine and remove the add-on, execute the following command:


    $ minishift addons remove satellite-registration --addon-env "SATELLITE_CA_URL=<CA_LOCATION>" --addon-env "SATELLITE_ORG=<ORG_NAME>" --addon-env "SATELLITE_ACTIVATION_KEY=<ACTIVATION_KEY>"

<a name="uninstall-add-on"></a>
### Uninstall add-on
To uninstall the addon from the addon list:


    $ minishift addons uninstall satellite-registration

