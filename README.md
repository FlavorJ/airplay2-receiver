# Experimental

Very quick python implementation of AP2 protocol using **minimal
multi-room** features without authentication/encryption.

**This code is experimental. To use for debugging purposes only.** 

---

## Raspberry Pi 4

Install docker and then build the image:

```zsh
docker build -f docker/Dockerfile -t invano/ap2-receiver .
```

To run the receiver:

```zsh
docker run -it --rm --device /dev/snd --net host invano/ap2-receiver
```


## macOS Catalina

To run the receiver please use Python 3 and do the following:

* Clone https://github.com/macosforge/alac.git somewhere to ALAC
* Copy `ap2/alac/apple_alac.cpp` and `ap2/alac/apple_alac.h` inside `ALAC/codec/` 
* Apply `ap2/alac/alac.patch` to `ALAC`
* build `ALAC` and copy the newly created `libalac.dylib` to `ap2/alac/`
* Run the following commands

```zsh
brew install python3
brew install portaudio
virtualenv -p /usr/local/bin/python3 proto
source proto/bin/activate
pip install -r requirements.txt
pip install --global-option=build_ext --global-option="-I/usr/local/Cellar/portaudio/19.6.0/include" --global-option="-L/usr/local/Cellar/portaudio/19.6.0/lib" pyaudio


python ap2-receiver.py -m myap2
```

* the AirPlay 2 receiver is announced as **myap2**.


---

Tested on Python 3.7.5 / macOS 10.15.2 with iPhone X 13.3 and Raspberry Pi 4

### Protocol notes

https://emanuelecozzi.net/docs/airplay2

