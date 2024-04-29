# Audio

The Kumquat offers two 3.5mm TRS jacks to access the audio interface. This document will demonstate how to play and record audio using the alsa-utils.

| Location | Color | Description   | Pinout                                                 |
| -------- | ----- | ------------- | ------------------------------------------------------ |
| Xn       | Green | Headphone Out | ![Headphone Connector Pinout](placeholder_image_link)  |
| Xn       | Pink  | Microphone In | ![Microphone Connector Pinout](placeholder_image_link) |

![Audio Connector Locations](placeholder_image_link)

## Prerequisites
Before you begin, make sure you have the following:

- Headphones or Headset with 3.5mm Audio connector
- Microphone with 3.5mm Audio connector

## Hardware Setup

- Connect the Headphones or Headset to the green Headphone jack on the Kumquat
- Connect the Microphone to the pink Microphone jack on the Kumquat

## Playing Audio

- First copy an audio file onto the device. In this example the wget command, which requires an internet connection, will be used. You can however use other methods to copy an audio file onto the device.
- Use the following command to download an audio file onto the device.

```sh
wget http://www2.cs.uic.edu/~i101/SoundFiles/PinkPanther60.wav
```

- Enable the audio output using the following command

```sh
amixer -c 0 sset 'Headphone',0 50% on
```

- Play the audio file.

```sh
aplay PinkPanther60.wav
```

## Recording Audio

- Enable the microphone input using the following command

```sh
amixer -c 0 sset 'Mic1',0 50% on cap
```

- Record the audio file

```sh
arecord -d 10 -f cd -t wav recording.wav
```

- Playback the recording using "aplay"

```sh
aplay recording.wav
```

## Playing Internet Radio

- Enable the audio output using the following command

```sh
amixer -c 0 sset 'Headphone',0 50% on
```

- Play a internet stream using mpv

```sh
mpv --demuxer-readahead-secs=5 --demuxer-max-bytes=4M --demuxer-max-back-bytes=2M --audio-buffer=5 http://radio4.cdm-radio.com:8020/stream-mp3-Chill_autodj
```