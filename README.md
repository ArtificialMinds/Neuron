#The Cortex API.

This repository is intended for use by Cortex developers, to build your own connected devices by defining Cortex device logic to execute in the cloud.

See contributing below for details on how to be a part of this project.

## Registering Cortex devices

When a Cortex device first boots, it will ask Neuron for an identifying code. This is done via the [Registration service][code-registration].

The device can now assign its public and private IPs to Neuron with its identifier. This can be done every time the network changes.

Once a device is tracked in this manner, it can securely send and receive data to Neuron.

Registration only needs to happen once per device.

## Controlling a device via Neuron

Cortex devices that are to be controlled via the web or via the [Cortex-App][app] need to have a Control Link initiated between the controller and the device itself.

For security reasons this can only be done from within the same network as the device.

To obtain a Control Link, ensure where you are sending the Neuron request from is on the network of the device, then reboot your Cortex device. Cortex devices enter a 30 second pairing phase on boot.

Next, send a request to `neuron.cortexiot.com/pair`. The request will take between 30 and 60 seconds to respond. When a response is returned, you will receive a JSON object representation of all pairing devices on your **local network**, which you can use to send and receive data between Neuron and the device.

## Neuron commands

New commands can be added to extend the capabilities of the Neuron by [submitting a pull request]. The following base commands are available:

+ addEventListener - Trigger an Output on Neuron when the device emits the provided event.
+ Set - Set the provided output on the device to the provided value.
+ Get - Get the value of the provided input from the device.

## Building

All processing is done using Neuron. Cortex devices act as lightweight IoT endpoints, and are typically going to be run on low-powered devices that don't have that much internet connectivity or processing power of their own. Instead of processing on the devices themselves, inputs are transmitted to Neuron, Neuron performs processing, and then transmits the output back to the device.

The distribution is hosted on Cortex servers, but can be developed against locally when building new connected devices.

Once a Neuron is developed fully, it can be shared into this repository in the form of a [pull request][github-pr].

## Running locally

[Composer][composer] is used to manage code dependencies. Once Composer is installed, you can quickly get set up by running `composer install` from the project's root directory.

Within the root directory there is a `src/Endpoint` directory, containing subdirectories for every API endpoint, by name.


[githuib-pr]: https://help.github.com/articles/about-pull-requests/
[composer]: https://getcomposer.org

[code-registration]: https://github.com/ArtificialMinds/Neuron