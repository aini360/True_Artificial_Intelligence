## 播放单声道wav 文件

- 使用FFmpeg
    - 树莓派apt安装的，不行，需要从源代码安装
        - [FFmpeg 在树莓派上的运行](http://blog.csdn.net/applelppa/article/details/25655335)
        - [树莓派安装ffmpeg（主要用于you-get视频的合并）](https://aoenian.github.io/2016/12/01/installFfmpegOnRasp/)
    - 使用
        - ffmpeg -i little_apple.mp3 -acodec pcm_s16le -ar 44100 -ac 1 little_apple2.wav
        - mono单声道，stereo双声道
```bash
(.py3) pro:wav_files play$ file  little_apple2.wav
little_apple2.wav: RIFF (little-endian) data, WAVE audio, Microsoft PCM, 16 bit, mono 44100 Hz
(.py3) pro:wav_files play$ file  little_apple.wav
little_apple.wav: RIFF (little-endian) data, WAVE audio, Microsoft PCM, 16 bit, stereo 44100 Hz

(env) pi@aiy:~/voice-recognizer-raspi/wav_files$ aplay little_apple.wav
Playing WAVE 'little_apple.wav' : Signed 16 bit Little Endian, Rate 44100 Hz, Stereo
^CAborted by signal Interrupt...
aplay: pcm_write:1940: write error: Interrupted system call

(env) pi@aiy:~/voice-recognizer-raspi/wav_files$ aplay running.wav
Playing WAVE 'running.wav' : Signed 16 bit Little Endian, Rate 16000 Hz, Mono
^CAborted by signal Interrupt...
aplay: pcm_write:1940: write error: Interrupted system call
```

- python代码
```python
import aiy.audio
TEST_SOUND_PATH = '/usr/share/sounds/alsa/Front_Center.wav'
aiy.audio.play_wave(TEST_SOUND_PATH)
#
fl='../wav_files/running.wav'
aiy.audio.play_wave(fl)
#
fl='../wav_files/little_apple2.wav'
aiy.audio.play_wave(fl)
```

- 播放【网易云音乐】
    - 下载
```bash
git clone https://github.com/ziwenxie/netease-dl
cd netease-dl/
python3 setup.py install
```        

- 使用
    
```bash
netease-dl song --name "Ballade Pour Adeline"

file Ballade\ Pour\ Adeline.mp3
Ballade Pour Adeline.mp3: Audio file with ID3 version 2.3.0, contains:MPEG ADTS, layer III, v1, 192 kbps, 44.1 kHz, Stereo

(.py3) pro:Downloads play$ mpg123 Ballade\ Pour\ Adeline.mp3
High Performance MPEG 1.0/2.0/2.5 Audio Player for Layers 1, 2 and 3
	version 1.25.7; written and copyright by Michael Hipp and others
	free software (LGPL) without any warranty but with best wishes


Terminal control enabled, press 'h' for listing of keys and functions.

Playing MPEG stream 1 of 1: Ballade Pour Adeline.mp3 ...

MPEG 1.0 L III cbr192 44100 j-s

Title:   Ballade pour Adeline                            Artist: Richard Clayderman
Album:   Ballade Pour Adeline
Year:    1993
```        