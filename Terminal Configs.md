# minty pi

Tags: On hold
steps: CAD

# OLD SPI display

<aside>

## Parts

https://www.adafruit.com/product/5462

https://www.adafruit.com/product/5613

## Driver

[https://github.com/juj/fbcp-ili9341](https://github.com/juj/fbcp-ili9341)

[https://github.com/balena-labs-projects/fbcp](https://github.com/balena-labs-projects/fbcp)

[https://github.com/notro/fbtft](https://github.com/notro/fbtft)

[https://github.com/tasanakorn/rpi-fbcp](https://github.com/tasanakorn/rpi-fbcp)

[https://github.com/notro/fbtft?tab=readme-ov-file](https://github.com/notro/fbtft?tab=readme-ov-file)

</aside>

<aside>

| ILI9341 Pin | Raspberry Pi GPIO Pin | Description |
| --- | --- | --- |
| VCC | 3.3V | Power supply |
| GND | GND | Ground |
| CS | GPIO 8 (SPI0 CE0) | Chip Select |
| RESET | GPIO 25 (or any GPIO) | Reset |
| DC (RS) | GPIO 24 | Data/Command |
| MOSI | GPIO 10 (SPI0 MOSI) | Master Out, Slave In |
| SCK | GPIO 11 (SPI0 SCLK) | Serial Clock |
| MISO | GPIO 9 (SPI0 MISO) | (Optional, not needed) |
| LED (Backlight) | 3.3V (or via GPIO) | Backlight |
</aside>

```python
sudo apt-get install cmake
cd ~
git clone https://github.com/juj/fbcp-ili9341.git
cd fbcp-ili9341
mkdir build
cd build
cmake -DILI9341=ON -DARMV8A=ON -DGPIO_TFT_DATA_CONTROL=25 -DGPIO_TFT_RESET_PIN=24 -DGPIO_TFT_BACKLIGHT=23 ..
make -j
sudo ./fbcp-ili9341
```

```python
# For Killing existing driver
sudo pkill fbcp
```

```c
sudo modprobe fbift_device custom name=fb_ili9341 gpios=reset:25,dc:24,led:18 speed= 16000000 bgr= 1

```

```c
#for the joystick

void setup() {
  pinMode(0, INPUT_PULLUP);
  pinMode(1, INPUT_PULLUP);
  pinMode(2, INPUT_PULLUP);
  pinMode(3, INPUT_PULLUP);

  pinMode(23, INPUT_PULLUP);
  pinMode(22, INPUT_PULLUP);
  pinMode(21, INPUT_PULLUP);
  pinMode(20, INPUT_PULLUP);
}

void loop() {
  // read analog inputs and set X-Y position
  //Joystick.X(analogRead(0));
  //Joystick.Y(analogRead(1));

  // read the digital inputs and set the buttons
  Joystick.button(1, digitalRead(0));
  Joystick.button(2, digitalRead(1));
  Joystick.button(3, digitalRead(2));
  Joystick.button(4, digitalRead(3));

  Joystick.button(5, digitalRead(23));
  Joystick.button(6, digitalRead(22));
  Joystick.button(7, digitalRead(21));
  Joystick.button(8, digitalRead(20));

  // a brief delay, so this runs 20 times per second
  delay(50);
}

```

DSI diplay - https://www.amazon.com/dp/B0BZCXQ2MK?ref=nb_sb_ss_w_as-reorder_k0_1_21&amp=&crid=LTX1N5NMKIKT&amp=&sprefix=waveshare+dsi+display

Adafruit soft tactile buttons - https://www.adafruit.com/product/3101?gad_source=1&gclid=CjwKCAiA34S7BhAtEiwACZzv4QKmWiX5ZjkQMhPYV1vqvoIKs9K6pd9nRCOj4pRJwga88SlbQ3fHrxoCE0oQAvD_BwE

Teensy LC (or other board for contoller) - https://www.pjrc.com/teensy/teensyLC.html

5V Lipo charge boost board (or other) - https://www.adafruit.com/product/2465