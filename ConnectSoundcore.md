# Connect soundcore bluetooth headphones to raspberry pi 4/ ubuntu:
you can find info [here](https://askubuntu.com/questions/1339765/replacing-pulseaudio-with-pipewire-in-ubuntu-20-04)

and like this, the genral idea is to replace Pulseaudio with Pipewire.


##Installation:
First, you need to install PipeWire and its associated libraries. Open your terminal and run the following commands:

```
sudo apt update
sudo apt install pipewire pipewire-pulse pipewire-audio-client-libraries
```

## Stop PulseAudio:
You should stop the PulseAudio service before proceeding with PipeWire. Run the following commands:

```
systemctl --user --now stop pulseaudio.socket
systemctl --user --now stop pulseaudio.service
```
## Enable and Start PipeWire:
To enable and start PipeWire, run the following commands:
```
systemctl --user --now enable pipewire.socket
systemctl --user --now enable pipewire.service
```
