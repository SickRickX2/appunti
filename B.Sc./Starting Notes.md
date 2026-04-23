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
>The **Channel State Information** **(CSI)** is an alternative and
>more fine-grained wireless communication channel 
>measurement than the RSSI metric. It's widely used in 
>modern wireless communication systems based on 
>OFDM, it obtains detailed signal propagation 
>characteristics from the transmitter to the receiver at the 
>subcarrier level. Transmissions can be adapted to the 
>current link conditions enabling reliable communications 
>in **multiple-input multiple-output (MIMO)** antenna 
>configuration:  
>![[Pasted image 20260423150244.png|300]]
>>[!tip] CSI Informations
>>It contains:
>>- *phase* -> refers to the **specific position or timing of 
>>a waveform** in its cycle relative to a reference point, 
>>typically measured in degrees or radians
>>- *amplitude* -> refers to the **peak value** or **maximum 
>>magnitude** of a signal, representing how far the signal 
>>moves from its baseline (zero) during each cycle (
>>**strenght or intensity** of the signal)
>>- *frequency* -> refers to the **number of cycles** a signal 
>>completes **per second** and is measured in Hertz (Hz)

### CSI Mathematical Structure
>[!note] CFR
>*CFR channel frequency response* is defined as: 
>$$ 
>H(f;t) = \int_{-\infty}^{\infty} h(\tau,t)e^{-
>j2\pi f \tau} d\tau = \sum_{i} a_i(t)e^{-j2\pi f 
>\tau_i(t)} = |H(f;t)|e^{j\angle H(f;t)}
>$$
>
>where $|H(f;t)|$ and $\angle H(f;t)$ indicate the 
>signal amplitude and phase responses respectively, and j 
>is the imaginary component


The CSI is a frequency-domain evaluation measure involving the CFR values computed for all the K OFDM-based subcarriers related to each p ∈ P packet reaching the receiver. Given Θ and Γ arrays of fixed receiving and transmitting antennas placed in a static environment, respectively, for each subcarrier k ∈ K over the wireless communication established between the θ ∈ Θ and γ ∈ Γ antennas, the frequency response $H(f)_k^{\theta, \gamma}$  can be specified as: 
$$
H(f)_k^{\theta,\gamma} = |H(f)_k^{\theta,\gamma}|e^{j\angle H(f)_k^{\theta,\gamma}}
$$
where $|H(f)_k^{\theta,\gamma}|$ is the signal amplitude and $j\angle H(f)_k^{\theta,\gamma}$ is the signal phase, while $j$ is the imaginary component resulting from the *Fourier transformation* applied to the impulse response.
The final CSI measurement estimated over all the K subcarriers,
considering all the antennas in the TX and RX arrays, is a complex matrix of size Θ × Γ × K, defined as:
$$ CSI = \begin{bmatrix} H(f)_1^{(1,1)} & H(f)_2^{(1,1)} & \dots & H(f)_\kappa^{(1,1)} \\ H(f)_1^{(1,2)} & H(f)_2^{(1,2)} & \dots & H(f)_\kappa^{(1,2)} \\ \vdots & \vdots & \vdots & \vdots \\ H(f)_1^{(\theta,\gamma)} & H(f)_2^{(\theta,\gamma)} & \dots & H(f)_\kappa^{(\theta,\gamma)} \end{bmatrix} $$
where $H(f)_k^{\theta,\gamma}$ is a signed 8-bit complex number indicating the κ-th subcarrier CFR value over the θ ∈ Θ and γ ∈ Γ antennas.

>[!warning] Fourier Transform
>In simple terms, the **Fourier Transform** is a mathematical tool that takes a complex, messy radio signal and breaks it down into its individual pure frequencies—allowing a receiver to perfectly separate and analyze the overlapping data streams (like our OFDM subcarriers).

