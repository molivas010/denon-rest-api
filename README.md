# denon-rest-api

## Summary
This application creates a REST API that can be used to send commands to a Denon AV receiver over
a network connection. This was tested with my Denon AVR-E300, but should be compatible with other
Denon network-attached receivers.

## Running in Docker
The included Dockerfile will install the dependencies and run on an Ubuntu image. You must set the
ADDRESS environment variable to the IP address of the receiver you want to connect to. Port 8000
is exposed by default.

In order to build the docker image use something similar to the following

docker build -t <name_of_tag> .
docker build -t my_denon_app .

Once the image is built you can run it with a command similar to the following

docker run -env ADDRESS=<YOUR_DENON_IP> -d -p 8000:8000  -t my_denon_app
docker run -env ADDRESS=192.168.0.25 -d -p 8000:8000 -t my_denon_app

## Running from comamnd line
1) Navigate to the root of this project in the command line.
1) Install Node (http://nodejs.org) and execute `npm install`.
2) Run `node . [ip address of receiver] [optional port]` to launch the web server. Port 8000 is used by default.

## Executing commands
Send GET requests to http://localhost:[port]/api/[command]

## Examples
``` Javascript
'http://localhost:8000/api/SIDVD'     //Sets Input to DVD   
'http://localhost:8000/api/SITUNER'   //Sets Input to TUNER   
'http://localhost:8000/api/PWON'      //turns PoWer ON   
```

## Notes
- The full list of valid commands is available in the included protocol PDF from Denon.
- You may need to adjust settings on your receiver to allow remote network control of your device.
- This application communicates with the receiver via the factory-provided telnet API.
