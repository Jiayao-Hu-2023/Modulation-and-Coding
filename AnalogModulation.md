# Understanding Analog Modulation: AM, DSB, SSB, PM, and FM

<img width="1400" height="1540" alt="image" src="https://github.com/user-attachments/assets/aba9a742-9253-43f0-896c-36412bd49956" />

---

## 1. Why Modulate?

A message signal $m(t)$ (voice, audio, sensor data) occupies low frequencies (baseband) and cannot be radiated efficiently. **Modulation** embeds the message into a high-frequency **carrier**

$$c(t) = A_\mathrm{c}\cos(2\pi f_\mathrm{c} t + \phi), \qquad f_\mathrm{c} \gg f_\mathrm{m},$$

by varying one of the carrier's three parameters — amplitude, phase, or frequency — according to $m(t)$. The general modulated signal is written as

$$s(t) = A(t)\cos\theta(t),$$

with **instantaneous frequency**

$$f_\mathrm{i}(t) = \frac{1}{2\pi}\frac{\mathrm{d}\theta(t)}{\mathrm{d}t}.$$

**Purposes of modulation:**

1. **Antenna size** — practical antennas need length $\approx \frac{\lambda}4$; a $1 \text{ kHz}$ signal would need $\sim 75 \text{ km}$, a $1 \text{ MHz}$ carrier only $\sim 75 \text{m}$.
2. **Frequency-division multiplexing (FDM)** — stations share the medium via distinct carriers.
3. **Noise immunity** — FM trades bandwidth for a large SNR improvement.
4. **Radiation/propagation** — high-frequency signals propagate and amplify efficiently.

Throughout we use a sinusoidal message $m(t) = A_\mathrm{m}\cos(2\pi f_\mathrm{m} t)$ for illustration; results generalize by replacing $f_\mathrm{m}$ with the message bandwidth $W$.

---

## 2. Amplitude Modulation

Amplitude modulation family: the carrier's *amplitude* is varied by $m(t)$ while the phase stays fixed. There are three canonical members: **DSB-LC** (large carrier = "ordinary AM"), **DSB-SC** (suppressed carrier), and **SSB** (single sideband).

### 2.1 DSB-LC ("Ordinary" AM) — Time Domain

$$s_\mathrm{AM}(t) = A_\mathrm{c}\left[1 + k_\mathrm{a} m(t)\right]\cos(2\pi f_\mathrm{c} t).$$

For sinusoidal $m(t)$, the **modulation index** is

$$\mu = k_\mathrm{a} A_\mathrm{m} \qquad \left(= \frac{A_\mathrm{m}}{A_\mathrm{c}} \text{ when } k_\mathrm{a} = \frac{1}{A_\mathrm{c}}\right),$$

so that $s_\mathrm{AM}(t) = A_\mathrm{c}\left[1 + \mu\cos(2\pi f_\mathrm{m} t)\right]\cos(2\pi f_\mathrm{c} t).$

**Envelope condition:** distortionless envelope detection requires $\mu \le 1$; $\mu > 1$ causes *overmodulation* (the dashed envelope in the time-domain figure folds over).

### 2.2 DSB-LC — Frequency Domain and Bandwidth

Using the product-to-sum identity,

$$s_\mathrm{AM}(t) = A_\mathrm{c}\cos(2\pi f_\mathrm{c} t) + \frac{\mu A_\mathrm{c}}{2}\cos\big[2\pi(f_\mathrm{c} + f_\mathrm{m})t\big] + \frac{\mu A_\mathrm{c}}{2}\cos\big[2\pi(f_\mathrm{c} - f_\mathrm{m})t\big].$$

The spectrum contains exactly **three components**: the carrier at $f_\mathrm{c}$ and two sidebands at $f_\mathrm{c} \pm f_\mathrm{m}$.

$$B_\mathrm{AM} = 2f_\mathrm{m} \quad (\text{twice the highest message frequency}).$$

All information sits in the sidebands; the carrier carries none but enables a trivial receiver.

### 2.3 Power and Efficiency of DSB-LC

$$P_\mathrm{c} = \frac{A_\mathrm{c}^2}{2}, \qquad P_\mathrm{t} = P_\mathrm{c}\left(1 + \frac{\mu^2}{2}\right), \qquad P_\mathrm{SB} = \frac{\mu^2}{2}P_\mathrm{c}.$$

**Modulation efficiency:**

$$\eta = \frac{P_\mathrm{SB}}{P_\mathrm{t}} = \frac{\mu^2}{2 + \mu^2}, \qquad \eta_{\max} = \frac{1}{3} \approx 0.33 \text{ at } \mu = 1.$$

Two-thirds of the transmitted power is wasted in the carrier — the motivation for the suppressed-carrier variants below.

### 2.4 DSB-SC (Double-Sideband Suppressed Carrier)

Simply multiply message and carrier:

$$\boxed{s_\mathrm{DSB}(t) = A_\mathrm{c} m(t)\cos(2\pi f_\mathrm{c} t)}$$

**Spectrum** (by the modulation theorem of the Fourier transform):

$$S_\mathrm{DSB}(f) = \frac{A_\mathrm{c}}{2}\left[ M(f - f_\mathrm{c}) + M(f + f_\mathrm{c}) \right],$$

where $M(f) = \mathcal{F}\{m(t)\}$. Key facts:

- **No carrier line** — all power is in the sidebands: $\eta = 100$%.
- Same bandwidth as DSB-LC: $B = 2f_\mathrm{m}$.
- Envelope is $|m(t)|$, **not** $m(t)$ — the envelope flips sign with $m(t)$, so envelope detection fails; **coherent (synchronous) detection is mandatory** (Section 5.2).
- Generated with a balanced mixer/multiplier; also recoverable as AM with $\mu \to \infty$.

### 2.5 SSB (Single-Sideband)

Transmit only one sideband — upper (USB) or lower (LSB):

$$B_\mathrm{SSB} = f_\mathrm{m}, \qquad P_\mathrm{SSB} = \tfrac{1}{2}P_\mathrm{DSB},$$

i.e., **half the bandwidth and half the power** of DSB for the same information.

**Spectrum:** 

$$S_\mathrm{SSB}(f) = \frac{A_\mathrm{c}}{4}\left[M(f-f_\mathrm{c}) + M(f+f_\mathrm{c})\right] \mp \frac{A_\mathrm{c}}{4j}\left[M(f-f_\mathrm{c})\mathrm{sgn}(f-f_\mathrm{c}) - M(f+f_\mathrm{c})\mathrm{sgn}(f+f_\mathrm{c})\right]$$

— one sideband of each shifted replica is cancelled.

**The Hilbert transform.** SSB's clean time-domain description needs the **Hilbert transform** $\hat m(t)$ of the message, defined as the message convolved with $\frac{1}{\pi t}$:

$$\hat m(t) = \mathcal{H} \{m(t)\} = m(t) * \frac{1}{\pi t} = \frac{1}{\pi}\int_{-\infty}^{\infty} \frac{m(\tau)}{t - \tau} \mathrm{d}\tau,$$


with frequency response a $-90^\circ$ phase shifter:

$$
H(f) = -j \mathrm{sgn}(f) = \begin{cases}
-j, & f \gt 0,\\
0, & f = 0,\\
j, & f \lt 0.
\end{cases}
$$

(In words: every positive-frequency component is shifted by $-90^\circ$, every negative-frequency one by $+90^\circ$; amplitudes are unchanged.)

**SSB time-domain expressions (phasing method):**

$$\boxed{s_\mathrm{SSB}(t) = m(t)\cos(2\pi f_\mathrm{c} t) \mp \hat m(t)\sin(2\pi f_\mathrm{c} t)}$$

where the **upper sign ($-$) gives USB and the lower sign ($+$) gives LSB**.

*Why it works:* writing $s(t) = \mathrm{Re}\{[m(t) \pm j\hat m(t)] e^{j2\pi f_\mathrm{c} t}\}$, the pre-envelope $m(t) \pm j\hat m(t)$ has a one-sided spectrum (its negative/positive half is removed by the Hilbert phase shifts), so the shift to $\pm f_\mathrm{c}$ leaves only one sideband.

**Generation methods:**
1. **Filter method** — generate DSB and steeply filter out one sideband (practical for $f_\mathrm{c} \gg f_\mathrm{m}$).
2. **Phasing method** — directly implement the boxed formula with two multipliers and a wideband $90^\circ$ phase-difference network.
3. **Weaver method** — quadrature mixing at a low intermediate frequency, relaxing the phase-shifter requirement.

**Demodulation:** coherent only (Section 5.2) — the SSB envelope is not proportional to $m(t)$. With a pilot carrier inserted, a modified envelope detector can also be used.

---

## 3. Angle Modulation: PM and FM

**Concept:** keep the amplitude constant and vary the *angle* $\theta(t)$ of the carrier.

- **Phase modulation (PM):** the message drives the **phase** directly.
- **Frequency modulation (FM):** the message drives the **frequency** directly — i.e., the phase is the *integral* of the message.

Both are **constant-envelope**: $$P = \frac{A_\mathrm{c}^2}{2}$$ regardless of $m(t)$ — a decisive advantage over AM.

### 3.1 Phase Modulation

$$s_\mathrm{PM}(t) = A_\mathrm{c}\cos\big[2\pi f_\mathrm{c} t + k_\mathrm{p} m(t)\big],$$

with **phase sensitivity** $k_\mathrm{p}$ (rad per unit message). The instantaneous frequency follows the *derivative* of the message:

$$f_\mathrm{i}(t) = f_\mathrm{c} + \frac{k_\mathrm{p}}{2\pi}\frac{\mathrm{d}m(t)}{\mathrm{d}t}.$$

PM therefore emphasizes high-frequency message content (and high-frequency noise).

### 3.2 Frequency Modulation

$$s_\mathrm{FM}(t) = A_\mathrm{c}\cos\left[2\pi f_\mathrm{c} t + 2\pi k_\mathrm{f} \int_0^t m(\tau)\, d\tau\right],$$

with **frequency sensitivity** $k_\mathrm{f}$ (Hz per unit message). The instantaneous frequency *is* the message:

$$f_\mathrm{i}(t) = f_\mathrm{c} + k_\mathrm{f}\, m(t).$$

FM's phase deviation is proportional to the *integral* of $m(t)$, emphasizing low-frequency content.

### 3.3 Deviation, Modulation Index, Bandwidth

For $m(t) = A_\mathrm{m}\cos(2\pi f_\mathrm{m} t)$:

$$\Delta f = k_\mathrm{f} A_\mathrm{m} \quad \text{(peak frequency deviation)},$$

$$\beta = \frac{\Delta f}{f_\mathrm{m}}  \text{(FM modulation index)}, \qquad \beta_\mathrm{p} = k_\mathrm{p} A_\mathrm{m}  \text{(PM index)}.$$

- **Narrowband FM ($\beta \ll 1$):** spectrum resembles AM — carrier plus two small sidebands, $B \approx 2f_\mathrm{m}$.
- **Wideband FM:** infinitely many sidebands at $f_\mathrm{c} \pm n f_\mathrm{m}$ with amplitudes $J_n(\beta)$ (Bessel functions of the first kind) — the multi-line "comb" in the spectrum figure.

**Carson's rule:**

$$B_\mathrm{FM} \approx 2(\Delta f + f_\mathrm{m}) = 2(\beta + 1)f_\mathrm{m}.$$

---

## 4. Demodulation: Recovering the Message

Demodulation is the inverse operation: extract $m(t)$ from $s(t)$. Each modulation family has its natural detector.

### 4.1 AM Envelope Detection (DSB-LC)

The simplest detector in radio: a **diode + RC low-pass** (possibly with a DC-blocking capacitor).

- The diode rectifies the RF; the capacitor charges to the envelope and discharges slowly between peaks.
- Choose the time constant to follow the message but smooth the carrier:

$$\frac{1}{f_\mathrm{c}} \ll RC \ll \frac{1}{f_\mathrm{m}}.$$

- Output: $v(t) \approx A_\mathrm{c}\left[1 + k_a m(t)\right]$; blocking the DC term recovers $m(t)$.
- **Requirement:** $\mu \le 1$ (else envelope foldover). Cost: one diode, one capacitor — why AM broadcast receivers are dirt cheap.

### 4.2 Coherent (Synchronous) Detection — DSB-SC, SSB, precise AM

Multiply the received signal by a **local carrier replica** $2\cos(2\pi f_\mathrm{c} t + \phi_\mathrm{e})$ and low-pass filter:

$$\hat m(t) = \mathrm{LPF}\{ s(t)\cdot 2\cos(2\pi f_\mathrm{c} t + \phi_\mathrm{e}) \}.$$

**Worked example — DSB-SC:** with $s(t) = m(t)\cos(2\pi f_\mathrm{c} t)$,

$$2m(t)\cos^2(2\pi f_\mathrm{c} t) = m(t) + m(t)\cos(4\pi f_\mathrm{c} t) \xrightarrow{\text{LPF}} m(t).$$


The double-frequency term is rejected; the factor 2 restores unit gain.

**Synchronization errors:**
- **Phase error $\phi_\mathrm{e}$:** output becomes $m(t)\cos\phi_\mathrm{e}$ — a pure gain loss; at $\phi_\mathrm{e} = \pi/2$ the output vanishes (*quadrature nulling*).
- **Frequency error $\Delta f$:** output is $m(t)$ multiplied by a slowly rotating phasor $e^{j2\pi\Delta f t}$ — audible beating; intolerable beyond a few Hz.

The local carrier is recovered with a **Costas loop** (for DSB-SC/BPSK-like signals) or from a transmitted **pilot tone**. AM can also be coherently demodulated; the result is identical to ideal envelope detection but requires sync — which is why envelope detection is preferred for broadcast.

### 4.3 FM Demodulation

Goal: turn frequency variations back into amplitude variations, then detect amplitude. Three classical methods:

**(a) Discriminator (differentiator + envelope detector).** Differentiate the FM wave:

$$\frac{\mathrm{d}s_\mathrm{FM}(t)}{\mathrm{d}t} = -A_\mathrm{c}\left[2\pi f_\mathrm{c} + 2\pi k_\mathrm{f} m(t)\right]\sin\big[2\pi f_\mathrm{c} t + 2\pi k_\mathrm{f} \int_0^t m(\tau)d\tau\big].$$

This is an **AM–FM wave**: its envelope is $\left|\,A_\mathrm{c}\left[2\pi f_\mathrm{c} + 2\pi k_\mathrm{f} m(t)\right]\right|$. A standard envelope detector recovers $f_\mathrm{c} + k_\mathrm{f} m(t)$; DC-blocking yields $k_\mathrm{f} m(t)$. (Practical discriminators implement the differentiation with a tuned slope circuit or a **Foster–Seeley** transformer.)

**(b) PLL (phase-locked loop).** The VCO tracks the input phase $\theta_\mathrm{i}(t) = 2\pi f_\mathrm{c} t + 2\pi k_\mathrm{f} \int m\,dt$; when locked, the VCO control voltage is

$$v_\mathrm{ctrl}(t) \propto \frac{\mathrm{d}}{\mathrm{d}t}\big[\theta_\mathrm{i}(t) - \theta_\mathrm{vco}(t)\big] \propto m(t).$$

Quiet and easy to integrate — the dominant modern FM demodulator.

**(c) Quadrature detector / zero-crossing counting** — count zero crossings per unit time $\Rightarrow$ instantaneous frequency.

**Why FM is quiet:** demodulated noise power grows quadratically with frequency, while message power is flat; **pre-emphasis/de-emphasis** networks (boost highs at the transmitter, cut them at the receiver) exploit this. Above threshold, the FM improvement factor is

$$\frac{(S/N)_o}{(S/N)_b} = 3\beta^2(\beta+1),$$

i.e., wideband FM buys ~ $10\lg \big[3\beta^2(\beta+1)\big]$ dB of SNR at the price of bandwidth — below the **threshold** (carrier-to-noise $\lesssim 10$ dB), however, clicks and dropouts suddenly appear.

### 4.4 PM Demodulation

PM can be demodulated with a **phase detector**: multiply by a quadrature carrier $2\sin(2\pi f_\mathrm{c} t)$ and low-pass filter. Using $\cos A \sin B = \tfrac12\big[\sin(A+B) - \sin(A-B)\big]$ with $A = 2\pi f_\mathrm{c} t + k_\mathrm{p} m(t)$, $B = 2\pi f_\mathrm{c} t$:

$$2s_\mathrm{PM}(t)\sin(2\pi f_\mathrm{c} t) = A_\mathrm{c}\sin\big[4\pi f_\mathrm{c} t + k_\mathrm{p} m(t)\big] - A_\mathrm{c}\sin\big[k_\mathrm{p} m(t)\big] \xrightarrow{\text{LPF}} -A_\mathrm{c}\sin\big(k_\mathrm{p} m(t)\big) \approx -A_\mathrm{c} k_\mathrm{p} m(t),$$

exact for small phase deviation $k_\mathrm{p} m(t) \ll 1$ rad. Alternatively, **differentiate PM to get FM** ($\frac{\mathrm{d}}{\mathrm{d}t}$ converts phase deviation into frequency deviation) and FM-detect, or use a PLL. Note the duality: differentiating PM gives FM; integrating FM gives PM — the practical reason commercial "FM" transmitters often PM-modulate at low frequency and integrate by low-pass filtering (Armstrong indirect method).

---

## 5. Comparison Summary

| Property | DSB-LC (AM) | DSB-SC | SSB | PM | FM |
|---|---|---|---|---|---|
| Varying parameter | Amplitude | Amplitude (no carrier) | Amplitude (one sideband) | Phase | Frequency |
| $s(t)$ | $A_\mathrm{c}[1+\mu m]\cos\omega_\mathrm{c} t$ | $A_\mathrm{c} m(t)\cos\omega_\mathrm{c} t$ | $m\cos\omega_\mathrm{c} t \mp \hat m\sin\omega_\mathrm{c} t$ | $A_\mathrm{c}\cos[\omega_\mathrm{c} t + k_\mathrm{p} m]$ | $A_\mathrm{c}\cos[\omega_\mathrm{c} t + 2\pi k_\mathrm{f} \int m]$ |
| Bandwidth | $2f_\mathrm{m}$ | $2f_\mathrm{m}$ | $f_\mathrm{m}$ | $\approx 2(\beta_\mathrm{p}{+}1)f_\mathrm{m}$ | $2(\Delta f + f_\mathrm{m})$ |
| Constant envelope? | No | No | No | Yes | Yes |
| Detection | Envelope (simplest) | Coherent | Coherent | Phase detector / diff + FM demod | Discriminator / PLL |
| Efficiency | $33$% | $100$% | $100$% | — | — |
| Noise immunity | Poor | Medium | Medium | Good | Excellent (above threshold) |
| Typical use | AM broadcast (0.5–1.7 MHz) | Stereo pilot, instrumentation | HF aeronautical/marine, telephony FDM | Indirect FM gen., digital PSK ancestor | FM broadcast (88–108 MHz), two-way radio |

**Memory hook:** *AM moves the envelope; PM moves the zero crossings via the message itself; FM moves the zero crossings via the integral of the message — and PM/FM never change the envelope.*

---

## 6. Takeaways

1. **DSB-LC** = ordinary AM: trivial envelope detection, but $\eta \le 33$% and $B = 2f_\mathrm{m}$.
2. **DSB-SC** removes the wasteful carrier: $s(t) = A_\mathrm{c} m(t)\cos\omega_\mathrm{c} t$, $\eta = 100$%, but demands coherent detection.
3. **SSB** halves bandwidth again to $f_\mathrm{m}$ via the Hilbert transform: $s(t) = m(t)\cos\omega_\mathrm{c} t \mp \hat m(t)\sin\omega_\mathrm{c} t$.
4. **PM/FM** are constant-envelope angle modulations; FM's bandwidth follows Carson's rule, $B \approx 2(\Delta f + f_\mathrm{m})$, and buys $\approx 3\beta^2(\beta+1)$ SNR improvement above threshold.
5. **Demodulation mirrors modulation:** envelope detection inverts envelope variation; coherent multiplication inverts mixing; differentiation (or a PLL) inverts integration — and integrating FM recovers PM, differentiating PM recovers FM.
6. Digital modulation (QAM, PSK, FSK) is the direct descendant of these three analog ideas.
