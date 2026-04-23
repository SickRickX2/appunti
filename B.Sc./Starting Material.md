## Orthogonal Frequency-Division Multiplexing

The *Orthogonal Frequency-Division Multiplexing* it's a **signal modulation** used by most of the modern wireless communications in order to transmit data encoded on multiple orthogonal carrier frequencies (**subcarries**) within the same individual communication channel.

By applying any data modulation scheme to a pure carrier wave, the signal's energy expands beyond its central frequency. This physical process generates **sidebands**—adjacent frequency ranges located just above and below the main carrier. 

In a densely packed multiple-carrier scenario, these sidebands naturally expand and overlap with neighboring subcarriers. Without specific countermeasures, this spectral overlap creates severe **inter-carrier interference (ICI)** at the overlapping frequencies. The *orthogonal* nature of **OFDM** is specifically designed to solve this issue, allowing subcarriers to overlap safely without their sidebands disrupting the data decoding process at the receiver.
Therefore, the receiver can recover the original
signal correlating the known set of orthogonal sinusoids without interference despite the overlapping sidebands.

>[!note] RSSI
>RSSI Received Signal Strength Indicator indicates the realtive signal quality capturing the wireless channel strenght variations. It s formally measured in decibels (dB) and generally expressed following the *log-distance path loss* model: 
>$$
>PL_d = PL_{d_0} + 10n \log_{10} \frac{d}{d_0} + \chi
$$

>[!note] CSI
>The **Channel State Information** **(CSI)** is an alternative and more fine-grained wireless communication channel measurement than the RSSI metric. It's widely used in modern wireless communication systems based on OFDM, it obtains detailed signal propagation characteristics from the transmitter to the receiver at the subcarrier level.

