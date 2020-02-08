# Ben Schroth Audio Reactive LED Strip
In my living room at my house I installed audio reactive LED lights to visualize music coming from my speakers.

# Changes to original repository
## Inspiration
The original code written by ([https://github.com/scottlawsonbc](Scott Lawson)) only visualized the audio input and when there wasn't audio input the LED's would scroll and change colors. My living room did not have an overhead light so I wanted the lights to be used as the lights for the room as well as an audio visualizer. The idea was to edit the code to when there was no audio input, the lights would stay a consistent color and act as the lights for the room.

## What I changed
This is an overview of the changes I made to the original repository.

- In ([config.py]config.py) there is a variable called `MIN_VOLUME_THRESHOLD = 1e-7`.
  - I checked the average volume by printing the volume of the microphone input stream. I found that with no input the volume was around 0.3. There was a small amount of volume because of the bluetooth receiver I use and my speakers.
  - I changed `MIN_VOLUME_THRESHOLD = 0.3` so that when there is no music playing the pixels would be a consistent color.
- The main script ([visualization.py]visualization.py) uses ([led.py]led.py) to set the color of each pixel.
  - ([led.py](led.py)) uses a library ([https://github.com/jgarff/rpi_ws281x.git]rpi_ws281x) to communicate with the LED's.
  - ([https://github.com/jgarff/rpi_ws281x.git]rpi_ws281x) has a function called `setPixelColor(n, red, green, blue)` to set the color of a pixel on the led strip.
    - n = Position of LED
    - r, g, b = RGB value of the pixel
  - I added a function called `NoAudio()` in ([led.py]led.py) that iterates through each pixel of the strip and sets the color to the desired color.
  - Then call `strip.show()` to display the pixels.
- The main script ([visualization.py](visualization.py)) visualizes the audio input (`microphone_update()`). If the volume was below the threshold it would scroll through colors.
  - I removed the scrolling effect and called `strip.NoAudio()` to set the desired color when there is no input to the pixels.

# What I learned
This is the first time I have made changes to an existing repository to fit my needs.\n
I learned how to SSH into a Raspberry Pi to make changes to the code already on the device because it is in an area that can't be used.\n
I learned how to fork an exisiting repository and post my chnages on GitHub.\n
I displayed that I can read someone's existing code and how it works to be able to make the chnages I wanted to make.\n

# Overview
The repository includes everything needed to build an LED strip music visualizer (excluding hardware):

- Python visualization code, which includes code for:
  - Recording audio with a microphone ([microphone.py](python/microphone.py))
  - Digital signal processing ([dsp.py](python/dsp.py))
  - Constructing 1D visualizations ([visualization.py](python/visualization.py))
  - Sending pixel information to the ESP8266 over WiFi ([led.py](python/led.py))
  - Configuration and settings ([config.py](python/config.py))
- Arduino firmware for the ESP8266 ([ws2812_controller_esp8266.ino](arduino/ws2812_controller_esp8266/ws2812_controller_esp8266.ino))

# License
This project was developed by Scott Lawson and is released under the MIT License.
