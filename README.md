# ESP32_CYD_455kHz_SDR
ESP32 2,8" CYD board receiver for 455kHz IF. Transforms conventional MW/SW radios to SDR with AM,FM and SSB 

Standard ESP32 modules can sample analog pins with I2S built-in ADC mode with sampling frequencies higher then 1Mhz. In this project I am using this capability
to sample 455kHz IF output signal of whatever MW/SW radio. Even oldest often abandoned radios like popular transistors that receive and demodulate only AM signals can become a receiver for AM/FM/LSB and USB signals. Furthermore all popular display features like stations specter and waterfall can run simultaneously with touch control over same display.
How this works: 455kHz signal on last IF transformer is strong enough (up to 1Vpp) to be sampled directly with analog pin of ESP32. To get necessary I and Q signals typical for decoding with DSP process in an SDR radio I decided to sample with 390kHz. The alias frequency is therefore 455kHz - 390kHz = 65kHz. By Nyquist this can become an 32,5kHz SDR radio. In order to run all DSP process I down sample the I2S buffer with factor of 12. 390kHz/12 is again 32,5kHz therefore this can work. Produced audio samples are output to built-in DAC converter of same ESP32. With this approach the system does not require a Tayloe mixer!

Hardware needed:
- Popular 2,8" CYD also has an audio amplifier onboard. Some  boards require to change resistors which define audio gain, otherwise the sound gets quickly distorted.
  Important!!!  Use display with ILI9341 driver! The code will not work with other drivers on display!
- 4 to 8 ohms speaker directly connected to SP connector on display board
- Display analog pin 35 needs a bias of about 1,6V. Make this with couple of 10k resistors connected to 3V3 and GND.
- Small 47pF to 100pF capacitor to connect on IF transformer just before the D1 demodulation diode in receiver. Use thin coaxial cable to connect to display pin35.

Optional hardware:
The project allows to connect an Si5351 to replace the conventional radio oscillator. This way the reception becomes more stable and SSB signals will sound cleaner.
RF connection of Si5351 output should again be realized using coaxial cable and capacitor. Disable radio oscillator in this case.
Instead of MW/SW radio an AM CB radio can be used to extend it to FM and SSB demodulation mode.

The code will compile in Arduino IDE. Tested with SDK core 2.0.17.

Link to YouTube video:

Some pictures of display appearance:
