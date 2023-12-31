# Digital-Comm-Lab-2
## Introduction
This lab was similar to the previous one in that GNURadio was used with an SDR except instead of scanning AM frequencies the audio file provided scanned FM frequencies. A flowchart was created in GNURadio to use the provided audio file to scan different frequencies on the frequency spectrum. Afterwards the SDR was connected to scan different radio frequencies in real time. The flowchart created is shown below.
## Flowchart
![image](https://github.com/blee0730/Digital-Comm-Lab-2/assets/130094173/e246764e-a6f0-4979-b66a-15bef7bf93e1)
This is the entire flowchart used in this lab that will be broken down into pieces and explained.

![image](https://github.com/blee0730/Digital-Comm-Lab-2/assets/130094173/8cc2eb71-0c61-4b89-8605-d56bd6bcd533)

The start of the flowchart is again similar to the first lab where multiple modules combine into one SDR module where the audio file gets replaced with real time radio frequencies. The filtering gets done by the SDR module as well so the previous filter is no longer needed and is instead integrated into the SDR block. There is also a frequency sink which shows the radio signals in the frequency domain as the SDR picks up the signals.
### Demodulator
![image](https://github.com/blee0730/Digital-Comm-Lab-2/assets/130094173/aefb3ce1-c10d-49d1-8068-97e19fb9a71a)

The FM Demod block is the frequency demodulator that converts the complex FM signal into a float with a channel rate of 400kHz which is the sampling frequency of the demodulator. This makes it so the complex frequency signal can be read by the computer. The decimation rate is at 1 so that none of the signal is lost in the process of demodulation. The audio pass and stop is the low pass filter that starts the cuttoff at 15kHz and ends at 16kHz giving it a transition width of 1kHz because it is difficult to create a brick wall low pass filter.

#### Low Pass Filter
![image](https://github.com/blee0730/Digital-Comm-Lab-2/assets/130094173/4309f710-7347-4b2e-8640-7d61d2014443)

This is the low pass filter that is being implemented by the Demodulator as shown by GnuRadio's Filter Design Tool. The cutoff frequency is at 15kHz with the end at 16kHz for a 1kHz transition width using the Hamming Window.
### Resampler
![image](https://github.com/blee0730/Digital-Comm-Lab-2/assets/130094173/9fbe3b38-6425-49e0-93bc-baa813d24585)

The rational resampler changes the sampling rate of the system to match the sampling rate of the computer. The resampling can only happen with an integer which is why the resampler must be interpolated and decimated by the sampling rate of the system and the sampling rate of the computer. This was also explained for the previous lab.

#### Decimation
![image](https://github.com/blee0730/Digital-Comm-Lab-2/assets/130094173/4d71f73c-a888-4de5-bc4e-13e7c3f8b823)

This is an example of what happens if there is too much decimation. The signal above is the message signal that needs to be captured and the signal below is the signal after decimation. The decimation changes the signal so much that it is unrecognizable on the output. Something similar happens during interpolation that changes the signal as well. While information is not lost during interpolation, it still creates false information that is transmitted leading to a different output. This is why correctly decimating and interpolating the signal is so important and why, if done wrong, it can lead to a unrecognizable message on the output.

### Output
![image](https://github.com/blee0730/Digital-Comm-Lab-2/assets/130094173/87ecf4c2-16a3-4cb3-ab55-763549509ea4)

On the output there is a waterfall representation of the radio station frequency in time on the very top as well as the fft of the original signal on the very bottom and demodulated audio signal in the middle. There are sliders on top to control the overall volume and gain of the system as well as a slider to change what frequency is being demodulated. Using this flowchart with the SDR and a list of FM radio stations in Colorado, it is easy to tune in to any FM radio station on the frequency spectrum.
