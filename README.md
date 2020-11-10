# Virtualmic

This minimal script creates a PulseAudio source and pipes a media file or stream into it.

## Dependencies

- [PulseAudio](https://www.freedesktop.org/wiki/Software/PulseAudio/)
- [FFmpeg](http://ffmpeg.org/)
- any POSIX compliant shell
- [mktemp](https://www.gnu.org/software/coreutils/mktemp) (optional, not needed when `virtualmic` is run with `-p filename`)

## Usage

```
Usage: virtualmic [-p pipe_filename] [-n source_name] [-f format]
       [-r rate] [-c channels] [-v] [-d] [-h] [input_filename]

  input_filename  This file is piped to the virtual mic (can be an url) (default: stdin)
  -p, --pipe      Set audio pipe filename (use mktemp otherwise)
  -n, --name      Set PulseAudio source_name (default: virtualmic)
  -f, --format    Set audio format (default: s16le)
  -r, --rate      Set audio sampling frequency (default: 44100)
  -c, --channels  Set number of audio channels (default: 1)
  -v, --verbose   Make output verbose
  -d, --default   Set virtual microphone as PulseAudio default source
  -h, --help      Show this help
```

## Examples

The most basic example is to use an audio file as virtual microphone:
```
virtualmic file.mp3
```

`virtualmic` reads from stdin by default:
```
<command that generates audio> | virtualmic
```

## Use any smartphone as microphone

I wrote this script initially to use my smartphone as mic after the sound card on my laptop got broken.

For this to work you first need to install an app on your phone to broadcast audio,
I'm using [IP Webcam](https://play.google.com/store/apps/details?id=com.pas.webcam&hl=en_US&gl=US) on Android.
When you run the app on your phone, you can connect to it with `virtualmic`.

With an IP Webcam URL, this is what the command looks like:
```
virtualmic 192.168.0.5:8080/audio.opus
```

There will of course be some latency, but the latency due to `virtualmic` should be very little.
