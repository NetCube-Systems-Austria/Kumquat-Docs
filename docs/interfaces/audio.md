# Audio

The Kumquat offers two 3.5mm TRS jacks to access the audio interface. This document will demonstate how to play and record audio using the alsa-utils.

| Location | Color                                              | Description   | Pinout                                                 |
| -------- | -------------------------------------------------- | ------------- | ------------------------------------------------------ |
| X8       | ![Lime](../../img/interfaces/audio/jack-lime.png)  | Headphone Out | ![Headphone Connector Pinout](../../img/interfaces/audio/pinout-headphone.png)  |
| X9       | ![Pink](../../img/interfaces/audio/jack-pink.png)  | Microphone In | ![Microphone Connector Pinout](../../img/interfaces/audio/pinout-microphone.png) |

![Audio Connector Locations](../../img/interfaces/connectors.png)

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

```
wget http://www2.cs.uic.edu/~i101/SoundFiles/PinkPanther60.wav
```

- Enable the audio output using the following command

```
amixer -c 0 sset 'Headphone',0 50% on
```

- Play the audio file.

```
aplay PinkPanther60.wav
```

## Recording Audio

- Enable the microphone input using the following command

```
amixer -c 0 sset 'Mic1',0 50% on cap
```

- Record the audio file

```
arecord -d 10 -f cd -t wav recording.wav
```

- Playback the recording using "aplay"

```
aplay recording.wav
```

## Playing Internet Radio

- Enable the audio output using the following command

```
amixer -c 0 sset 'Headphone',0 50% on
```

- Play a internet stream using mpv

```
mpv --demuxer-readahead-secs=5 --demuxer-max-bytes=4M --demuxer-max-back-bytes=2M --audio-buffer=5 http://radio4.cdm-radio.com:8020/stream-mp3-Chill_autodj
```

- Checkout [https://dir.xiph.org/](https://dir.xiph.org/) for other stream urls