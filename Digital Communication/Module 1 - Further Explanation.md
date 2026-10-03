---
course: DIGITAL COMMUNICATION
course_code: 24EC504
module: 1
type: detailed-study-notes
source: handwritten Module 1 notes + syllabus-aligned explanation
status: verified-and-expanded
---

# Module 1 — Further Explanation

> [!info] How to use this note
> This note expands the concepts in [[Module 1 - Introduction and Sampling]]. The handwritten notes remain the primary source for the terminology and topic order. The sections below add explanatory detail so that the ideas are easier to understand and reproduce in an examination.
>
> Syllabus reference: [[24EC504 - Digital Communication Syllabus]]

## 1. Introduction to Digital Communication

A communication system has one basic purpose: **transfer information from a source to a destination** through a physical or wireless channel.

A simple chain is:

```text
Information source
       ↓
Transmitter
       ↓
Communication channel
       ↓
Receiver
       ↓
Destination
```

In digital communication, the information is represented using discrete symbols, usually bits (`0` and `1`). An analog message such as speech can first be converted into a digital sequence using:

**Sampling → Quantization → Coding**

### Why are these three operations different?

- **Sampling:** makes the signal discrete in **time**. It tells us *when* the signal is measured.
- **Quantization:** makes the signal discrete in **amplitude**. It tells us *which allowed amplitude level* represents each sample.
- **Coding:** represents each quantized level using a binary word.

For example, if a quantizer has 8 allowed levels, each level can be represented using 3 bits because

$$
2^3=8.
$$

So an analog waveform becomes a sequence of binary words that can be processed and transmitted digitally.

> [!important] Remember
> Sampling concerns **time**, quantization concerns **amplitude**, and coding concerns **binary representation**.

---

## 2. Digital Communication System

The handwritten notes show a system containing source coding, channel coding, modulation, a communication channel, detection, channel decoding and source decoding.

![[Digital Communication/assets/digital-communication-system.svg]]

### Transmitter side

#### Source encoder

The source encoder converts the information into an efficient digital representation. The main idea is to remove **redundancy** that is not necessary for representing the source.

If a source produces symbols with unequal probabilities, an efficient source representation can use fewer bits on average for more probable symbols. The important point for this course is that source coding is associated with **efficient representation** and reduction of unnecessary information.

#### Channel encoder

A noisy channel can introduce errors. Channel coding deliberately adds structured redundancy so that the receiver can detect and/or correct some errors.

This gives an important contrast:

- Source coding → **removes redundancy**.
- Channel coding → **adds controlled redundancy**.

#### Modulator

The modulator converts the digital information into a waveform suitable for the physical channel. Depending on the system, information may be conveyed by changing amplitude, frequency or phase.

### Receiver side

The receiver performs the reverse operations:

1. Detect/demodulate the received waveform.
2. Use the channel decoder to deal with channel errors.
3. Use the source decoder to reconstruct the source representation.
4. Deliver the recovered information to the destination.

> [!tip] Exam point
> A common block-diagram question is to identify what happens at each block. Remember the order: **source → source encoder → channel encoder → modulator → channel → detector → channel decoder → source decoder → destination**.

---

## 3. Communication Channels

A communication channel is the medium through which the transmitted signal travels from transmitter to receiver.

The handwritten notes discuss telephone channels, coaxial cable, optical fibre and microwave radio.

### 3.1 Telephone channel

The notes use approximately **300 Hz to 3400 Hz** as the voice-band range.

A real channel does not necessarily transmit every frequency component with exactly the same gain and phase. Consequently, a transmitted signal can experience:

- amplitude distortion,
- phase distortion,
- attenuation, and
- noise/interference.

For digital transmission, these effects can change the received waveform enough to cause detection errors.

### 3.2 Coaxial cable

A coaxial cable has a central conductor, insulating material and an outer conducting shield.

The shield helps reduce the influence of external electromagnetic interference. Coaxial cables can support substantially greater bandwidth than ordinary telephone pairs, although practical performance depends on cable construction and frequency.

### 3.3 Optical fibre

An optical fibre has a **core** surrounded by **cladding**. The core has a higher refractive index than the cladding.

This index difference allows light to remain guided inside the fibre. Optical fibre provides very high bandwidth and is widely used for long-distance communication.

### 3.4 Microwave radio

Microwave links normally use directional antennas and require a suitable propagation path, commonly approximated as **line-of-sight**.

Because the signal travels through the atmosphere, obstacles and propagation conditions can affect the received signal.

---

## 4. Sampling Process

Let the continuous-time message be $g(t)$. Instead of retaining its value at every instant, we measure it at equally spaced instants:

$$
0,\;T_s,\;2T_s,\;3T_s,\ldots
$$

The corresponding samples are

$$
g(0),\;g(T_s),\;g(2T_s),\ldots
$$

The sampling frequency is

$$
f_s=\frac{1}{T_s}.
$$

If $T_s$ becomes smaller, samples are taken more frequently and $f_s$ becomes larger.

### Impulse-train model

The ideal sampled signal can be written as

$$
g_s(t)=\sum_{n=-\infty}^{\infty}g(nT_s)\delta(t-nT_s).
$$

This equation says that there is an impulse at every sampling instant and that the height/weight of that impulse equals the corresponding message-signal sample.

### Why use the impulse model?

It makes the mathematics of sampling simple. Multiplication of the signal by an impulse train produces a train of weighted impulses, and the Fourier transform then makes the repeated-spectrum property clear.

---

## 5. Spectrum of a Sampled Signal

One of the most important ideas in this module is:

> **Sampling in time produces periodic repetitions of the spectrum in frequency.**

If $G(f)$ is the spectrum of $g(t)$, then ideal sampling gives

$$
G_s(f)=\frac{1}{T_s}\sum_{n=-\infty}^{\infty}G(f-nf_s).
$$

The original spectrum appears around

$$
0,\;\pm f_s,\;\pm2f_s,\ldots
$$

The distance between adjacent spectral replicas is $f_s$.

### Why this matters

Suppose the original signal has maximum frequency $f_m$. Its baseband spectrum occupies approximately $-f_m$ to $+f_m$.

For perfect reconstruction, the first spectral replica must not overlap the original spectrum. This leads directly to the sampling theorem.

---

## 6. Sampling Theorem and Nyquist Criterion

For a band-limited signal whose highest frequency component is $f_m$, the sampling frequency must satisfy

$$
f_s\ge2f_m.
$$

The minimum theoretical sampling frequency,

$$
f_{s,\min}=2f_m,
$$

is called the **Nyquist rate**.

The corresponding maximum sampling interval is

$$
T_s\le\frac{1}{2f_m}.
$$

### Deriving the condition from the spectrum

The original spectrum extends up to $f_m$. The next copy starts at $f_s-f_m$.

For the two spectra not to overlap,

$$
f_m\le f_s-f_m.
$$

Therefore,

$$
2f_m\le f_s.
$$

Hence,

$$
\boxed{f_s\ge2f_m}.
$$

### Nyquist rate vs. Nyquist interval

These terms are easy to confuse:

- **Nyquist rate:** minimum required sampling frequency = $2f_m$.
- **Nyquist interval:** maximum permitted sampling period = $1/(2f_m)$.

> [!warning] Common mistake
> Do not write Nyquist rate as $f_m/2$. The rate is **twice** the highest signal frequency.

---

## 7. Reconstruction of the Original Signal

After sampling, the spectrum consists of repeated copies of the original spectrum. If the copies do not overlap, an ideal low-pass filter can select the original baseband copy.

Conceptually:

```text
Analog signal
     ↓
Sampler
     ↓
Sampled signal / repeated spectrum
     ↓
Ideal low-pass reconstruction filter
     ↓
Recovered analog signal
```

The reconstruction filter should:

1. pass the required message spectrum, and
2. reject the unwanted spectral replicas.

### Sinc interpolation

For an ideal band-limited signal, the reconstructed waveform can also be described using shifted sinc functions:

$$
g(t)=\sum_{n=-\infty}^{\infty}g(nT_s)
\operatorname{sinc}\left(\frac{t-nT_s}{T_s}\right).
$$

Each sample value acts as a weighting factor for one shifted sinc function. Adding all of them reconstructs the continuous waveform.

This is the mathematical explanation of why a set of properly spaced samples can represent the original band-limited signal.

---

## 8. Aliasing

**Aliasing** occurs when the sampling frequency is too low and the spectral replicas overlap.

The condition is

$$
f_s<2f_m.
$$

When overlap occurs, different continuous-time frequency components can produce the same sampled representation. Therefore, the original signal cannot be uniquely identified from the samples alone.

### Example

Suppose

$$
f_m=5\text{ kHz}.
$$

The minimum theoretical sampling rate is

$$
f_s=2(5)=10\text{ kHz}.
$$

If we sample at $8$ kHz, then

$$
8<10,
$$

so aliasing occurs.

### How aliasing is prevented

The two basic approaches are:

- sample at a sufficiently high rate, and
- use an **anti-aliasing low-pass filter** before sampling to remove frequency components above the permitted band.

> [!important]
> Aliasing is not simply “noise.” It is a sampling distortion caused by spectral overlap, and once the overlapping information has been lost, ordinary reconstruction filtering cannot uniquely restore the original signal.

---

## 9. Oversampling and Undersampling

### Undersampling

When

$$
f_s<2f_m,
$$

the signal is undersampled relative to the Nyquist requirement. For a general baseband signal this causes aliasing.

### Nyquist-rate sampling

When

$$
f_s=2f_m,
$$

the theoretical minimum rate is reached. In practical systems, some margin is normally desirable because real filters are not ideal.

### Oversampling

When

$$
f_s>2f_m,
$$

the spectral replicas have more separation. This can make practical filtering easier and can provide a transition/guard region for the anti-aliasing and reconstruction filters.

---

## 10. Quadrature Sampling of Band-Pass Signals

A band-pass signal does not have to be sampled in exactly the same way as a baseband signal. The handwritten notes introduce **quadrature sampling**, where a band-pass signal is represented using two components:

- **In-phase component ($g_I(t)$)**
- **Quadrature component ($g_Q(t)$)**

A common representation is

$$
g(t)=g_I(t)\cos(2\pi f_ct)-g_Q(t)\sin(2\pi f_ct).
$$

The cosine and sine carriers are separated by 90° in phase, which is why they are called quadrature carriers.

![[Digital Communication/assets/quadrature-sampling.svg]]

### Why two components?

A band-pass waveform can contain both amplitude and phase information around a carrier. Representing it with two orthogonal components allows the receiver to preserve this information in a convenient low-pass form.

### Basic operation

At the receiver, the signal can be multiplied by:

$$
\cos(2\pi f_ct)
$$

and

$$
\sin(2\pi f_ct)
$$

and then low-pass filtered. This separates the information into the in-phase and quadrature paths.

The two recovered components can then be combined to reconstruct the band-pass signal.

---

## 11. Practical Sampling

Ideal impulse sampling is a mathematical model. A practical sampler uses a switching element or sampling circuit that is active for a finite duration.

Therefore, practical sampled waveforms contain pulses rather than infinitely narrow impulses.

The handwritten notes discuss **natural sampling**, **sample-and-hold**, and **flat-top sampling**.

### Natural sampling

During each sampling pulse, the top of the output pulse follows the instantaneous shape of the input signal.

If the periodic sampling waveform is $c(t)$, the operation can be represented conceptually as

$$
g_s(t)=c(t)g(t).
$$

### Sample-and-hold

A sample-and-hold circuit first captures the input value and then holds that value approximately constant until the next sampling instant.

This is useful because subsequent circuits need a stable voltage for a finite amount of time while the conversion or processing takes place.

---

## 12. Flat-Top Sampling

In flat-top sampling, every sampled pulse has a flat top. Its amplitude represents the value of the input signal at the sampling instant.

Conceptually:

```text
Input signal:       /\       /\
                   /  \     /  \
                  /    \___/    \

Flat-top output:   ┌───┐       ┌───┐
                   │   │       │   │
                   └───┘       └───┘
```

The hold circuit maintains each sample value for a finite duration.

### Aperture effect

Because the input is not sampled at an infinitely short instant in a real circuit, the hold operation introduces frequency-dependent attenuation. This effect is called the **aperture effect**.

The result is that higher-frequency components can be attenuated more than lower-frequency components.

The handwritten notes therefore introduce equalization as part of practical signal recovery.

---

## 13. Equalization in Signal Recovery

The practical recovery chain described in the notes is:

**Sampled waveform → Sample-and-hold → Low-pass filter → Equalizer → Recovered analog waveform**

The low-pass filter performs the main spectral selection. The equalizer compensates, within the required frequency range, for amplitude distortion introduced by the sampling/hold process or channel.

### Why is equalization necessary?

Suppose the sampling/hold system attenuates some frequencies more than others. Even if the low-pass filter removes unwanted replicas, the remaining signal may not have the same amplitude response as the original.

An equalizer is designed to compensate for this known response.

> [!tip] Exam wording
> **Equalization compensates for amplitude/frequency-response distortion introduced by the practical sampling/hold system or channel.**

---

## 14. Pulse-Amplitude Modulation (PAM)

In PAM, the **amplitude** of each pulse is varied according to the corresponding sample value of the message signal.

![[Digital Communication/assets/pam.svg]]

The pulse timing and pulse width are kept according to the sampling structure, while pulse amplitude carries the sample information.

The waveform can be written as

$$
s(t)=\sum_{m=-\infty}^{\infty}g(mT_s)v(t-mT_s),
$$

where $g(mT_s)$ is the message value at the $m$th sampling instant and $v(t)$ represents the pulse shape.

### How to visualize PAM

If the message samples are

$$
2,\;5,\;3,\;7,
$$

then the corresponding PAM pulse amplitudes are proportional to

$$
2,\;5,\;3,\;7.
$$

Thus the information is contained in **pulse amplitude**.

### PAM and sampling

Sampling creates the sequence of sample values. PAM uses those values to control the amplitude of pulses for transmission.

This makes PAM an important bridge between the sampling topic and later pulse/digital communication concepts.

---

## 15. Time-Division Multiplexing (TDM)

TDM allows several independent signals to share the same communication channel by assigning each signal a different **time slot**.

![[Digital Communication/assets/tdm-system.svg]]

Suppose four signals are sampled periodically. Instead of transmitting all four samples simultaneously, the transmitter sends them one after another:

```text
Time →
| A1 | B1 | C1 | D1 | A2 | B2 | C2 | D2 | ... |
```

Here:

- `A1` = first sample of signal A
- `B1` = first sample of signal B
- etc.

The receiver uses synchronization to determine which time slot belongs to which signal.

### TDM steps

1. Band-limit each input signal.
2. Sample the signals sequentially.
3. Interleave the samples into time slots.
4. Transmit the combined sequence.
5. Synchronize the receiver with the transmitter.
6. Separate the samples belonging to each source.
7. Use reconstruction filters to recover the individual analog signals.

### Why TDM works with PAM

A PAM pulse occupies only a portion of the sampling interval. Therefore, different signals can use different portions of time without transmitting their pulses simultaneously.

### Synchronization

Synchronization is essential. If the receiver loses track of the slot positions, samples can be assigned to the wrong channels.

---

## 16. T1 Carrier

The handwritten notes connect TDM with telephone voice transmission using an **8 kHz sampling frequency**.

The sampling period is

$$
T_s=\frac{1}{8000}=125\;\mu s.
$$

Each voice channel is sampled 8000 times per second. If each sample is represented by 8 bits, then one channel requires

$$
8000\times8=64\text{ kbps}.
$$

For 24 channels, the basic payload rate is

$$
24\times64=1536\text{ kbps}=1.536\text{ Mbps}.
$$

The handwritten notes include an additional framing bit per frame, giving

$$
R=8000(24\times8+1)
$$

and therefore

$$
\boxed{R=1.544\text{ Mbps}}.
$$

This is the familiar **T1 carrier rate**.

The notes also discuss a 32-slot arrangement:

$$
R=8000(32\times8+1)=2.048\text{ Mbps}.
$$

> [!important] Numerical shortcut
> For T1-style calculations, remember: **8 kHz sampling × 8 bits/sample × 24 voice channels + framing overhead = 1.544 Mbps**.

---

## 17. Worked Nyquist-Rate Problem

Consider the message signal from the notes:

$$
m(t)=A\cos(2000\pi t)\cos(1000\pi t).
$$

Use the identity

$$
\cos A\cos B=\frac12[\cos(A+B)+\cos(A-B)].
$$

Therefore,

$$
m(t)=\frac{A}{2}\left[\cos(3000\pi t)+\cos(1000\pi t)\right].
$$

Convert angular frequency to frequency using

$$
f=\frac{\omega}{2\pi}.
$$

For $3000\pi$ rad/s:

$$
f_1=\frac{3000\pi}{2\pi}=1500\text{ Hz}.
$$

For $1000\pi$ rad/s:

$$
f_2=\frac{1000\pi}{2\pi}=500\text{ Hz}.
$$

The highest frequency is therefore

$$
f_m=1500\text{ Hz}.
$$

The Nyquist rate is

$$
f_s\ge2f_m=2(1500)=3000\text{ Hz}.
$$

So the minimum theoretical sampling rate is

$$
\boxed{f_s=3000\text{ Hz}}.
$$

![[Digital Communication/assets/nyquist-example.svg]]

### General method for these problems

1. Expand products of sine/cosine terms using trigonometric identities.
2. Find every frequency component.
3. Identify the highest frequency $f_m$.
4. Apply $f_s=2f_m$ for the minimum theoretical rate.
5. State units clearly.

---

# 18. Important Comparisons

| Concept | Meaning |
|---|---|
| Sampling | Converts a continuous-time signal into samples at discrete time instants |
| Quantization | Maps sample amplitudes to discrete permitted levels |
| Coding | Represents quantized levels using binary code words |
| Source coding | Removes unnecessary source redundancy for efficient representation |
| Channel coding | Adds controlled redundancy for error protection |
| PAM | Represents sample values through pulse amplitude |
| TDM | Shares one channel by assigning different time slots to different signals |
| Nyquist rate | Twice the highest frequency of a band-limited signal |
| Nyquist interval | Maximum sampling period corresponding to the Nyquist rate |
| Aliasing | Spectral overlap caused by insufficient sampling |
| Reconstruction filter | Recovers the original baseband spectrum from sampled data |
| Equalizer | Compensates for known amplitude/frequency-response distortion |
| Natural sampling | Pulse tops follow the input during the sampling interval |
| Flat-top sampling | Each sampled pulse is held approximately constant |
| Quadrature sampling | Uses in-phase and quadrature components for band-pass signals |

---

# 19. Formula Sheet

### Sampling

$$
f_s=\frac{1}{T_s}
$$

### Sampling theorem

$$
f_s\ge2f_m
$$

### Nyquist rate

$$
f_{Nyquist}=2f_m
$$

### Nyquist interval

$$
T_{Nyquist}=\frac{1}{2f_m}
$$

### Ideal sampled signal

$$
g_s(t)=\sum_{n=-\infty}^{\infty}g(nT_s)\delta(t-nT_s)
$$

### Sampled spectrum

$$
G_s(f)=\frac{1}{T_s}\sum_{n=-\infty}^{\infty}G(f-nf_s)
$$

### Quadrature representation

$$
g(t)=g_I(t)\cos(2\pi f_ct)-g_Q(t)\sin(2\pi f_ct)
$$

### PAM

$$
s(t)=\sum_{m=-\infty}^{\infty}g(mT_s)v(t-mT_s)
$$

### T1 rate from the handwritten-note arrangement

$$
R=8000(24\times8+1)=1.544\text{ Mbps}
$$

---

# 20. Examination Focus

For a short-answer or theory question, be prepared to explain:

- definition of digital communication,
- basic digital communication system blocks,
- source coding vs. channel coding,
- different communication channels,
- definition of sampling,
- impulse-train representation of sampling,
- spectrum of a sampled signal,
- sampling theorem,
- Nyquist rate and Nyquist interval,
- aliasing and how to prevent it,
- reconstruction using an LPF,
- quadrature sampling,
- natural sampling,
- flat-top sampling,
- sample-and-hold operation,
- aperture effect and equalization,
- PAM,
- TDM and synchronization,
- T1 carrier calculation.

For numerical problems, the most important workflow is:

**Find the highest frequency → apply $f_s\ge2f_m$ → calculate the required sampling period if asked.**

---

# 21. Quick Self-Test

- What is the difference between sampling and quantization?
- Why is the sampling frequency required to be at least twice the highest message frequency?
- What happens to the spectrum after ideal sampling?
- What is aliasing?
- Why can aliasing not be removed after spectral overlap has occurred?
- What is the function of the reconstruction low-pass filter?
- What is the difference between natural and flat-top sampling?
- Why is an equalizer used with practical sample-and-hold systems?
- What quantity is varied in PAM?
- Why is synchronization important in TDM?
- How is the 1.544 Mbps T1 rate obtained?
- For $m(t)=A\cos(2000\pi t)\cos(1000\pi t)$, what is the highest frequency and the Nyquist rate?
