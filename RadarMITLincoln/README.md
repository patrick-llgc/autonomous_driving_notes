# Radar Course from MIT Lincoln Lab
- Radar range resolution for a pulsed only depends on the bandwidth at c/2B. This does not depend on the wavelength.
## pulse compression
### Matched filtering: 
- The time-bandwidth product describes the increase in range resolution and signal-to-noise ratio (SNR) achieved by a pulse of a given band- and pulse-width over an unmodulated pulse of the same width.
	- 80 MHz BW means 1.9 meter range resolution
- For an unmodulated pulse, the time-bandwidth product is always 1. 
- Without windowing, the highest sidelobes after pulse compression will be 13 dB from the peak. 
	- This is a characteristic of all constant-modulus waveforms and is due to the fact that the Fourier Transform of a rectangular window is a sinc function (and sync functions have first sidelobes that are ~13 dB down from the carrier peak). 20 * log(sinc(1.5 * pi)) / log(10) = -13
- Linearly Frequency Modulated (LFM) waveform is also called a "chirp".
- LFM is doppler tolerant, and is suitable for detecting moving target. 

### Stretch processing
- Stretch processing allows your radar to use wideband waveforms at low sample rates, which increases range resolution at the expense of decreasing range extent.
- Linear Frequency Modulated (LFM) waveforms exhibit strong range/Doppler coupling – meaning that a shift in time/range is the same as a shift in frequency and vice versa. This allows us to measure range shifts by comparing the instantaneous frequencies of the transmit and receive waveforms.