---
course: DIGITAL COMMUNICATION
course_code: 24EC504
module: 1
type: study-notes
source: handwritten notes
status: verified
---

# Module 1 — Introduction to Digital Communication & Sampling

> [!info] Source
> These notes are transcribed from the uploaded handwritten **DC Module 1** notes. The original terminology and order are retained as closely as possible. Diagrams below are clean redrawings of the diagrams present in the handwritten notes.
>
> Syllabus reference: [[24EC504 - Digital Communication Syllabus]]

## 1. Introduction to Digital Communication

A communication system transfers information from a source to a destination through a communication channel.

### Analog and digital signals

- An **analog signal** is continuous in time and amplitude.
- A sinusoidal signal is characterized by quantities such as amplitude, frequency and phase.
- In a **digital system**, information is represented by a sequence of discrete symbols/bits.
- An analog message can be converted into digital form using operations such as **sampling, quantization and coding**.

The handwritten notes emphasize the advantages of digital communication systems, including improved flexibility, compatibility and reliability, and the ability to handle wideband channels used with satellite, optical-fibre and coaxial communication systems.

### Analog-to-digital conversion sequence

The notes describe the basic conversion chain as:

**Sampling → Quantization → Coding**

Sampling converts a continuous-time signal into a discrete-time representation. Quantization maps each sample to one of a finite number of amplitude levels. Coding represents the selected quantization level by a binary code word.

> [!important] Key idea
> Sampling makes time discrete; quantization makes amplitude discrete; coding represents the quantized values with bits.

---

## 2. Basic Signal Processing Operations in Digital Communication

The handwritten notes show a basic digital communication system containing:

- Digital source
- Source encoder
- Channel encoder
- Modulator
- Communication channel
- Detector
- Channel decoder
- Source decoder
- User/destination

The transmitter contains source coding, channel coding and modulation. The receiver performs detection/demodulation followed by channel and source decoding.

![[Digital Communication/assets/digital-communication-system.svg]]

### Source coding

The source encoder maps the digital source output into another digital representation. The notes identify the objective of source coding as reducing redundancy so that efficient transmission is possible and reducing the required bandwidth.

### Channel coding

Channel coding introduces controlled redundancy to improve reliable communication over a noisy channel. The channel decoder uses the received information to recover the transmitted sequence.

### Modulation

Modulation produces a physical waveform suitable for transmission through the channel. The carrier waveform can be varied in **amplitude, frequency or phase** according to the information-bearing signal.

---

## 3. Channels for Digital Communication

The handwritten notes discuss examples of communication channels.

### 3.1 Telephone channel

The telephone channel is described as a band-pass channel used for voice/data communication. The notes mention an approximate voice-band range of **300 Hz to 3400 Hz** and discuss amplitude and phase distortion and the resulting effect on data transmission.

### 3.2 Coaxial cable

A coaxial cable consists of a central conductor surrounded by an insulating material and an outer conducting shield. The notes identify advantages such as relatively high transmission bandwidth and reduced susceptibility to external interference.

### 3.3 Optical fibre

An optical fibre contains a **core** surrounded by **cladding**. The core has a slightly higher refractive index than the cladding, allowing light to propagate by repeated internal reflection.

### 3.4 Microwave radio

The notes describe microwave communication as using transmitting and receiving antennas placed sufficiently high for line-of-sight propagation. The operating frequency is in the microwave range, and obstructions can affect propagation.

> [!note]
> These channel descriptions are source-note material. They are included here because they occur in the handwritten Module 1 notes; they are not expanded beyond what is needed for the syllabus topic “Channels for Digital communication.”

---

# 4. Sampling Process

Sampling is the first major operation used when converting an analog signal into a digital representation.

Consider a continuous-time signal $g(t)$. Sampling converts it into a discrete-time signal by measuring its value at equally spaced time instants.

If the sampling period is $T_s$, the sampling frequency is

$$
f_s = \frac{1}{T_s}
$$

The sample values occur at

$$
t = 0,\; \pm T_s,\; \pm 2T_s,\ldots
$$

and are represented as $g(nT_s)$.

![[Digital Communication/assets/sampling-process.svg]]

### Impulse-train representation

The handwritten notes represent the sampling function using a train of impulses. The sampled signal is

$$
g_s(t)=\sum_{n=-\infty}^{\infty}g(nT_s)\,\delta(t-nT_s)
$$

where $\delta(t-nT_s)$ is a Dirac delta function located at $t=nT_s$.

Each impulse is weighted by the corresponding sample value of the original signal.

---

# 5. Spectrum of a Sampled Signal

Taking the Fourier transform of the sampled signal gives a periodic repetition of the original spectrum.

The notes give the sampled-spectrum relationship in the form

$$
G_s(f)=\frac{1}{T_s}\sum_{n=-\infty}^{\infty}G(f-nf_s)
$$

where

$$
f_s=\frac{1}{T_s}
$$

Thus, sampling in the time domain produces periodic spectral replicas in the frequency domain. The separation between adjacent replicas is $f_s$.

![[Digital Communication/assets/sampling-spectrum-aliasing.svg]]

### Band-limited signal condition

Suppose $g(t)$ is band-limited to a highest frequency $f_m$. To recover the original signal without spectral overlap, the sampling frequency must satisfy the Nyquist condition.

---

# 6. Sampling Theorem / Nyquist Sampling Criterion

> [!important] Sampling theorem
> A continuous-time signal can be completely represented by and recovered from its samples if the sampling frequency is greater than or equal to twice the highest frequency component of the message signal.

Therefore,

$$
f_s \ge 2f_m
$$

where $f_m$ is the highest frequency present in the message signal.

The **Nyquist rate** is

$$
f_{s,\min}=2f_m
$$

and the corresponding **Nyquist interval** is

$$
T_s \le \frac{1}{2f_m}
$$

### Why the condition is required

After sampling, copies of $G(f)$ occur at integer multiples of $f_s$. If $f_s$ is large enough, the copies remain separated and an appropriate reconstruction low-pass filter can isolate the original spectrum.

If the replicas overlap, the original spectrum cannot be separated perfectly. This distortion is called **aliasing**.

---

# 7. Reconstruction of a Message from Its Samples

The notes explain that the original analog signal can be recovered from its sampled representation by passing the sampled signal through an ideal low-pass reconstruction filter.

The reconstruction filter passes the original baseband spectrum while rejecting the unwanted spectral replicas around multiples of $f_s$.

For an ideal reconstruction filter, the passband is selected to include the original message spectrum but not the adjacent spectral replicas.

The notes also discuss the equivalent sinc-interpolation viewpoint: each sample can be associated with a shifted sinc function, and the original signal is reconstructed by adding the weighted shifted sinc functions.

A useful form is

$$
g(t)=\sum_{n=-\infty}^{\infty}g(nT_s)\,\operatorname{sinc}\left(\frac{t-nT_s}{T_s}\right)
$$

for ideal band-limited reconstruction.

> [!note]
> The equation above expresses the reconstruction principle represented in the handwritten derivation. The central exam point is the relationship between the sampled spectrum, the reconstruction low-pass filter, and the Nyquist condition.

---

# 8. Quadrature Sampling of Band-Pass Signals

The notes introduce quadrature sampling for a band-pass signal centered around carrier frequency $f_c$.

A band-pass signal can be represented using in-phase and quadrature components:

$$
g(t)=g_I(t)\cos(2\pi f_ct)-g_Q(t)\sin(2\pi f_ct)
$$

The two low-pass components can be obtained by multiplying the band-pass signal by cosine and sine carriers and then applying low-pass filters.

![[Digital Communication/assets/quadrature-sampling.svg]]

### Reconstruction

At the receiver, the sampled in-phase and quadrature components are reconstructed and combined after multiplication by the corresponding cosine and sine carriers.

The notes emphasize that quadrature sampling is used for band-pass signals and that the two components can be sampled separately.

---

# 9. Undersampling, Oversampling and Aliasing

The handwritten notes illustrate two important cases.

### Case 1 — Sampling below the required rate

If

$$
f_s < 2f_m
$$

spectral replicas overlap. This produces **aliasing**.

### Case 2 — Sampling above the Nyquist rate

If

$$
f_s > 2f_m
$$

there is a guard band between adjacent spectral replicas, making reconstruction easier.

> [!warning] Aliasing
> Once overlapping spectral components have occurred because of insufficient sampling, an ideal reconstruction filter cannot uniquely recover the original signal.

---

# 10. T1 Carrier / Time-Division Multiplexing

The handwritten notes discuss voice-signal multiplexing using a fixed sampling rate of **8 kHz**.

The sampling interval is

$$
T_s=\frac{1}{8000}=125\;\mu s
$$

A frame can contain either **24** or **32** time slots in the notes. Each time slot carries an 8-bit sample.

### 24-channel case

The notes calculate the signalling rate as

$$
R=8000(24\times8+1)
$$

which gives

$$
R=1.544\;\text{Mbps}
$$

This is the **T1 carrier** rate.

### 32-channel case

Similarly,

$$
R=8000(32\times8+1)
$$

which gives

$$
R=2.048\;\text{Mbps}
$$

The notes identify **1.544 Mbps** and **2.048 Mbps** as the two basic rates discussed in this section.

---

# 11. Practical Aspects of Sampling and Signal Recovery

The handwritten notes discuss practical sampling of a finite-duration analog signal using a periodic sampling function.

A sampling function can be represented by a sequence of rectangular pulses of period $T_s$. The sampled output is obtained by multiplying the input signal by the sampling function.

![[Digital Communication/assets/flat-top-sampling.svg]]

## Ordinary / natural sampling

In natural sampling, the top of each sampling pulse follows the instantaneous value of the input signal during the sampling interval.

The notes show:

$$
g_s(t)=c(t)g(t)
$$

where $c(t)$ is the periodic sampling function.

### Sampling-and-hold

The notes then discuss a sample-and-hold operation in which each sample value is held approximately constant for the required holding interval.

A sample-and-hold circuit therefore produces a sequence of constant-amplitude pulses corresponding to the sampled values.

---

# 12. Flat-Top Sampling

In **flat-top sampling**, the amplitude of each sampled pulse is held constant during the sampling interval.

The handwritten notes represent the hold pulse by

$$
h(t)=
\begin{cases}
1, & 0<t<T\\
0, & t<0\text{ and }t>T
\end{cases}
$$

and also express it using a rectangular-pulse form.

The flat-top process introduces a frequency-domain effect known as **aperture effect**. The sample-and-hold operation modifies the spectrum according to the frequency response of the hold circuit.

The notes show the sample-and-hold block concept as:

**Sampled waveform → Sample-and-hold circuit → output held waveform**

The practical reconstruction chain includes a low-pass filter and an equalizer. The equalizer compensates for the amplitude response introduced by the sample-and-hold process.

---

# 13. Equalization in Signal Recovery

The handwritten notes describe the recovery of the analog waveform using:

**Sampled waveform → Sample-and-hold → Low-pass filter → Equalizer → Analog waveform**

The equalizer is chosen to compensate for the amplitude response of the preceding sampling/hold process.

The notes explicitly state the equalizer response conceptually as being proportional to the inverse of the hold response over the required frequency band.

---

# 14. Pulse-Amplitude Modulation (PAM)

## Definition

In **pulse-amplitude modulation**, the amplitude of a periodic train of rectangular carrier pulses is varied in proportion to the instantaneous sample values of the message signal.

The handwritten notes describe PAM as having:

- constant pulse duration,
- varying pulse amplitude,
- pulse amplitude determined by the message-signal sample values.

![[Digital Communication/assets/pam.svg]]

If $v(t)$ denotes the carrier pulse, the notes give the PAM waveform as

$$
s(t)=\sum_{m=-\infty}^{\infty}g(mT_s)v(t-mT_s)
$$

where $g(mT_s)$ are the sample values and $T_s$ is the sampling period.

A rectangular pulse can be written as

$$
h(t)=
\begin{cases}
1, & 0<t<T\\
0, & t<0\text{ and }t>T
\end{cases}
$$

or represented using a shifted rectangular function.

> [!important] PAM vs. flat-top sampling
> The handwritten notes point out that PAM is closely related to flat-top sampling: the pulse amplitude is varied according to the sample value, while the pulse width is maintained over the pulse duration.

---

# 15. Time-Division Multiplexing (TDM)

An important feature of pulse-amplitude modulation is that the pulses occupy the communication channel only for part of each sampling interval. The unused portions of time can therefore be shared by other independent message signals.

This leads to **time-division multiplexing (TDM)**.

![[Digital Communication/assets/tdm-system.svg]]

### Basic TDM operation

1. Each input message is first band-limited using a low-pass / pre-alias filter.
2. A commutator samples the individual message signals sequentially.
3. The samples are interleaved into time slots.
4. The multiplexed sequence is transmitted through the common communication channel.
5. At the receiver, a synchronized decommutator separates the individual sample streams.
6. Individual low-pass reconstruction filters recover the message signals.

### Synchronization

The notes emphasize that the transmitter and receiver must operate synchronously so that the receiver can identify the correct time slot for each message.

### Channel distortion and equalization

The notes state that a TDM system can be sensitive to dispersion in the common channel. Equalization is therefore used to correct channel-induced dispersion and improve system operation.

---

# 16. Worked Nyquist-Rate Example from the Notes

The final handwritten page contains Nyquist-rate exercises.

For a product of cosine terms, use

$$
\cos A\cos B=\frac12[\cos(A+B)+\cos(A-B)]
$$

For the example written in the notes,

$$
m(t)=A\cos(2000\pi t)\cos(1000\pi t)
$$

using the product identity gives frequency components at

$$
\frac{2000\pi+1000\pi}{2\pi}=1500\text{ Hz}
$$

and

$$
\frac{2000\pi-1000\pi}{2\pi}=500\text{ Hz}.
$$

Therefore the highest frequency is $1500$ Hz and the Nyquist rate is

$$
f_s=2(1500)=3000\text{ Hz}.
$$

![[Digital Communication/assets/nyquist-example.svg]]

The notes also contain a second expression involving a sinc-type signal and identify the highest frequency component before applying the Nyquist-rate rule.

---

# 17. Quick Revision Sheet

| Topic | Key point |
|---|---|
| Sampling frequency | $f_s=1/T_s$ |
| Sampling theorem | $f_s\ge 2f_m$ |
| Nyquist rate | $2f_m$ |
| Nyquist interval | $1/(2f_m)$ |
| Sampled signal | $g_s(t)=\sum g(nT_s)\delta(t-nT_s)$ |
| Sampled spectrum | $G_s(f)=\frac1{T_s}\sum G(f-nf_s)$ |
| Aliasing | Spectral overlap caused by insufficient sampling |
| Quadrature representation | $g(t)=g_I(t)\cos(2\pi f_ct)-g_Q(t)\sin(2\pi f_ct)$ |
| T1 rate | $1.544$ Mbps |
| 32-channel rate in notes | $2.048$ Mbps |
| PAM | Pulse amplitude follows message sample value |
| Flat-top sampling | Sample amplitude is held approximately constant during the hold interval |
| TDM | Multiple message signals share one channel in separate time slots |

---

# 18. Syllabus Verification

The handwritten material was checked against the **24EC504 Module 1** syllabus.

### Directly covered in the notes

- Introduction to digital communication
- Sources and signals
- Basic signal-processing operations
- Channels for digital communication
- Sampling theorem
- Reconstruction from samples
- Sampling distortion / aliasing
- Practical aspects of sampling and signal recovery
- Quadrature sampling of band-pass signals
- TDM / T1 carrier

These correspond to the Module 1 syllabus topics in [[24EC504 - Digital Communication Syllabus]].

### Notes that extend within Module 1

The handwritten material goes into mathematical derivations of sampled spectra, reconstruction, practical sampling, flat-top sampling, PAM and TDM. These are treated here as supporting explanations of the syllabus topics rather than as separate syllabus modules.

### Practical/lab connection

The syllabus separately lists **verification of the sampling theorem using flat-top samples** as a laboratory experiment. The handwritten notes' discussion of natural/flat-top sampling and sample-and-hold therefore also supports the practical component.

---

# 19. Exam-Oriented Questions to Practise

- State and explain the sampling theorem.
- Derive the spectrum of a sampled signal.
- Explain aliasing with suitable frequency-domain diagrams.
- Explain reconstruction of an analog signal from its samples.
- Explain quadrature sampling of a band-pass signal.
- Explain natural sampling and flat-top sampling.
- Explain the aperture effect and the role of an equalizer.
- Define PAM and derive its waveform expression.
- Explain the operation of a TDM system with a block diagram.
- Derive the T1 carrier bit rate for 24 channels.
- Calculate the Nyquist rate and Nyquist interval for a given signal.

---

> [!tip] Study order
> **Introduction → Digital communication system → Channels → Sampling process → Sampling spectrum → Sampling theorem → Reconstruction → Quadrature sampling → Aliasing → Practical sampling → Flat-top sampling → PAM → TDM → Numericals**
