# Networking

## Background reading

Here are some background reading about networking and networking in Linux:

TODO: to write

Make sure that you know:

- what are IP addresses
- what are subnets
- how DNS works
- how `.local` names work
- ...

A short reference follows.



## Visualizing information about the network

### `ping`

TODO: to write

### `ifconfig`

TODO: to write

    $ ifconfig



# Wireless networks

### `iwlist`

What wireless networks do I have around?

    $ sudo iwlist ![interface] scan | grep SSID

Does the interface support 5 GHz channels?

    $ sudo iwlist ![interface] freq

Example output:

    wlx74da38c9caa0  20 channels in total; available frequencies :
      Channel 01 : 2.412 GHz
      Channel 02 : 2.417 GHz
      Channel 03 : 2.422 GHz
      Channel 04 : 2.427 GHz
      Channel 05 : 2.432 GHz
      Channel 06 : 2.437 GHz
      Channel 07 : 2.442 GHz
      Channel 08 : 2.447 GHz
      Channel 09 : 2.452 GHz
      Channel 10 : 2.457 GHz
      Channel 11 : 2.462 GHz
      Channel 36 : 5.18 GHz
      Channel 40 : 5.2 GHz
      Channel 44 : 5.22 GHz
      Channel 48 : 5.24 GHz
      Channel 149 : 5.745 GHz
      Channel 153 : 5.765 GHz
      Channel 157 : 5.785 GHz
      Channel 161 : 5.805 GHz
      Channel 165 : 5.825 GHz
      Current Frequency:2.437 GHz (Channel 6)

Note that in this example only *some* 5Ghz channels are supported (36, 40, 44, 48, 149, 153, 157, 161, 165); for example, channel 38, 42, 50 are not supported.
This means that you need to set up the router not to use those channels.
