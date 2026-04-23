****
## Orthogonal Frequency-Division Multiplexing
****

The *Orthogonal Frequency-Division Multiplexing* it's a **signal modulation** used by most of the modern wireless communications in order to transmit data encoded on multiple orthogonal carrier frequencies (**subcarries**) within the same individual communication channel.

By applying any data modulation scheme to a pure carrier wave, the signal's energy expands beyond its central frequency. This physical process generates **sidebands**,adjacent frequency ranges located just above and below the main carrier. 

In a densely packed multiple carrier scenario, these sidebands naturally expand and overlap with neighboring subcarriers. Without specific countermeasures, this spectral overlap creates severe **inter-carrier interference (ICI)** at the overlapping frequencies. The *orthogonal* nature of **OFDM** is specifically designed to solve this issue, allowing subcarriers to overlap safely without their sidebands disrupting the data decoding process at the receiver.
Therefore, the receiver can recover the original
signal correlating the known set of orthogonal sinusoids without interference despite the overlapping sidebands.
![[Pasted image 20260423150028.png|500]]

>[!note] RSSI
>RSSI Received Signal Strength Indicator indicates the realtive signal quality capturing the wireless channel strenght variations. It s formally measured in decibels (dB) and generally expressed following the *log-distance path loss* model: 
>$$
>PL_d = PL_{d_0} + 10n \log_{10} \frac{d}{d_0} + \chi
$$

>[!note] CSI
>The **Channel State Information** **(CSI)** is an alternative and more fine-grained wireless communication channel measurement than the RSSI metric. It's widely used in modern wireless communication systems based on OFDM, it obtains detailed signal propagation characteristics from the transmitter to the receiver at the subcarrier level. Transmissions can be adapted to the current link conditions enabling reliable communications in **multiple-input multiple-output (MIMO)** antenna configuration:  
>![[Pasted image 20260423150244.png|300]]
>>[!tip] CSI Informations
>>It contains:
>>- *phase* -> refers to the **specific position or timing of a waveform** in its cycle relative to a reference point, typically measured in degrees or radians
>>- *amplitude* -> refers to the **peak value** or **maximum magnitude** of a signal, representing how far the signal moves from its baseline (zero) during each cycle (**strenght or intensity** of the signal)
>>- *frequency* -> refers to the **number of cycles** a signal completes **per second** and is measured in Hertz (Hz)

### CSI Mathematical Structure
>[!note] CFR
>*CFR channel frequency response* is defined as: 
>$$ 
>H(f;t) = \int_{-\infty}^{\infty} h(\tau,t)e^{-j2\pi f \tau} d\tau = \sum_{i} a_i(t)e^{-j2\pi f \tau_i(t)} = |H(f;t)|e^{j\angle H(f;t)}
>$$
>where $|H(f;t)|$ and $\angle H(f;t)$ indicate the signal amplitude and phase responses respectively, and j is the imaginary component


