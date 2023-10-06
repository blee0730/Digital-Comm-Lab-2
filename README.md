# Digital-Comm-Lab-2
This lab was similar to the previous one in that GNURadio was used with an SDR except instead of scanning AM frequencies the audio file provided scanned FM frequencies. A flowchart was created in GNURadio to use the provided audio file to scan different frequencies on the frequency spectrum. Afterwards the SDR was connected to scan different radio frequencies in real time. The flowchart created is shown below.
## Flowchart
![image](https://github.com/blee0730/Digital-Comm-Lab-2/assets/130094173/e246764e-a6f0-4979-b66a-15bef7bf93e1)
This is the entire flowchart that will be broken down into pieces and explained.

![image](https://github.com/blee0730/Digital-Comm-Lab-2/assets/130094173/8cc2eb71-0c61-4b89-8605-d56bd6bcd533)

The start of the flowchart is again similar to the first lab where multiple modules combine into one SDR module where the audio file gets replaced with real time radio frequencies. The filtering gets done by the SDR module as well so the previous filter is no longer needed and is instead integrated into the SDR block. There is also a time sink which shows the frequency signal in the time domain as the SDR picks up the signals.
### Demodulator
![image](https://github.com/blee0730/Digital-Comm-Lab-2/assets/130094173/aefb3ce1-c10d-49d1-8068-97e19fb9a71a)

The FM Demod block is the frequency demodulator that converts the complex FM signal into a float with a channel rate of 400kHz which is the sampling frequency of the demodulator. This makes it so the complex frequency signal can be read by the computer. The decimation rate is at 1 so that none of the signal is lost in the process of demodulation. The audio pass and stop is the low pass filter that starts the cuttoff at 15kHz and ends at 16kHz giving it a transition width of 1kHz.
### Resampler
![image](https://github.com/blee0730/Digital-Comm-Lab-2/assets/130094173/9fbe3b38-6425-49e0-93bc-baa813d24585)

The rational resampler changes the sampling rate of the system to match the sampling rate of the computer. The resampling can only happen with an integer which is why the resampler must be interpolated and decimated by the sampling rate of the system and the sampling rate of the computer. This was also explained for the previous lab.
### Output
![image](https://github.com/blee0730/Digital-Comm-Lab-2/assets/130094173/87ecf4c2-16a3-4cb3-ab55-763549509ea4)

On the output there is a waterfall representation of the frequency spectrum on top as well as the fft of the original and demodulated audio signal. There are sliders on top to control the overall volume and gain of the system as well as a slider to change what frequency is being demodulated. Using this flowchart with the SDR and a list of FM radio stations in Colorado, it is easy to tune in to any FM radio station on the frequency spectrum.
