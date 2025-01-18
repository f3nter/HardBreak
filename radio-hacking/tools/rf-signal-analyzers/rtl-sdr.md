# RTL-SDR

## Theory

RTL-SDR stands for "RTL2832U Software Defined Radio." It is a low-cost USB device that can receive a wide range of radio frequencies, typically from about 500 kHz to 1.7 GHz. Originally designed for digital TV reception, RTL-SDR has become popular in the fields of amateur radio, signal analysis, and electronic surveillance due to its versatility and affordability.

The RTL2832U chip, which is the heart of the device, allows for software-defined radio capabilities by digitizing the received analog signals. By using appropriate software, users can decode various signal types, including FM, AM, SSB, and even digital modes. The flexibility of RTL-SDR lies in its ability to process signals using software running on a computer, enabling users to experiment with different modulation techniques, protocols, and applications without the need for specialized hardware.

## Usage

#### Spectrum Analysis

One common use case for RTL-SDR is spectrum analysis, which helps users visualize and analyze radio frequency signals in their environment. Here’s how a pentester might leverage RTL-SDR for this purpose:

* Setup
  * The pentester connects the RTL-SDR device to their laptop and installs software such as SDR# (SDRSharp) or GQRX.
* Antenna Selection
  * They choose an appropriate antenna based on the frequencies of interest, such as a dipole antenna for VHF/UHF bands.
* Scanning Frequencies
  * The pentester uses the software to scan a range of frequencies, looking for unexpected signals that could indicate unauthorized transmissions, like rogue wireless devices.
* Signal Analysis
  * By examining the spectrum display, they can identify active frequencies, measure signal strength, and even decode specific types of signals, such as wireless communications or telemetry data.

## Example with RTL-SDR

1. We can use the [Universal Radio Hacker](https://github.com/jopohl/urh)  + the RTL SDR to analyze the frequency
2. Let's assume we see two spikes in the frequency analyzer:

<figure><img src="../../../.gitbook/assets/image (64).png" alt=""><figcaption><p>Frequency Spectogram</p></figcaption></figure>

3. We can see that there are two spikes for the signal one at 868.039 MHz and one at 868.058 MHz, so the delta is 19 kHz and the deviation 9.5 kHz.
4. Next, we captured some signals with the RTL-SDR on that frequency of each sensor alone in order to analyze them
5. In the URH Interpretation we can play with the settings (Modulation, Error tolerance etc.) and we will get HEX-coded data back.
   1. Note: An encoding will probably be used, so don't expect to see raw ASCII&#x20;
   2. We are looking for an output, which will look like packets: So probably a static header part, size, and data
   3.  URH has also an automatic analyze function, which will try to find patterns in the recorded data:

       <figure><img src="../../../.gitbook/assets/image (69).png" alt=""><figcaption><p>Pattern detected</p></figcaption></figure>
6. If you can interpret the data, you may can intercept sensitive data.

## Resources

* [RTL SDR](https://www.rtl-sdr.com/)
* [Universal Radio Hacker Git Repository](https://github.com/jopohl/urh?tab=readme-ov-file)
