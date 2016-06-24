Control your EPSON projector connected vio USB or serial cable to your local computer or a remote machine.

Preparation
-----------

Install package `uucp` on the machine that is connected to the projector.

Usage
-----

```
  Usage: index [options] <connect-command>

  Options:

    -h, --help                output usage information
    -V, --version             output the version number
    -m, --model [model-name]  specify projctor model. Use "auto" to query REST API based on serial number. [auto]

```

Auto-Detect Projector Model
---------------------------
if you specify "auto" as model name (that's the default), the program will use this URL to lookup the projector's model name based on its serial number.
Privacy notice: The unique serial number of the device in question will be sent over the network as part of a URL.

If you prefer to query the web service manually or the host computer where the projector is connected does not have Internet access, you can use the follow command:

```
curl "http://www.epson.co.uk/gb/en/viewcon/corporatesite/modules/warranty_details/search?ajax=true&serial=<SERNO>" |json
```

Examples
--------

Control projector connected to serial port `ttyUSB0` on local machine:

```
escvp21 "cu -l /dev/ttyUSB0 -s 9600"
```

Control projector connected to serial port `ttyUSB0` on remote machine:

```
escvp21 "ssh -e none user@machine \"cu -l /dev/ttyUSB0 -s 9600\""
```

Example Output
--------------

```
$  escvp21 index.js "ssh -e none projectionist@cinema.local \"cu -l /dev/ttyUSB0 -s 9600\"" --power on
.response of SNO?: SNO=SPGF340554L
Projector identified as EH-TW8100
response of PWR ON:
response of LAMP?: LAMP=574
response of LUMINANCE?: LUMINANCE=01
response of BRIGHT?: BRIGHT=125
response of CONTRAST?: CONTRAST=125
response of TINT?: TINT=126
response of HREVERSE?: HREVERSE=ON
response of VREVERSE?: VREVERSE=OFF
response of MSEL?: MSEL=01
response of ASPECT?: ASPECT=00
response of PWR?: PWR=02
response of SOURCE?: SOURCE=30
```

