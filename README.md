# M-PSK & M-QAM Constellation and SER Simulation

A Python-based digital communication simulation that generates **QPSK, 8-PSK, 16-QAM, and 64-QAM** constellations, transmits symbols through an **AWGN channel**, performs **minimum-distance detection**, and evaluates **Symbol Error Rate (SER) versus SNR**.

---

## 📌 Project Overview

This project demonstrates the basic principles of digital modulation and symbol detection using Python.

The simulation includes:

* QPSK
* 8-PSK
* 16-QAM
* 64-QAM
* Gray-coded constellation generation
* Average-energy normalization
* AWGN channel simulation
* Minimum-distance symbol detection
* Constellation visualization
* SER calculation
* SER vs SNR performance analysis

The main goal is to understand how different modulation schemes behave in the presence of noise.

---

## 🎯 Objectives

The objectives of this experiment are:

1. Generate M-PSK and M-QAM constellations.
2. Apply Gray mapping to the constellation generation.
3. Normalize each constellation to unit average symbol energy.
4. Simulate an AWGN communication channel.
5. Detect received symbols using minimum Euclidean distance.
6. Visualize ideal and noisy constellation points.
7. Calculate Symbol Error Rate for different SNR values.
8. Compare the performance of different modulation schemes.

---

## 🛠️ Technologies and Libraries

### Programming Language

* Python 3.x

### Libraries Used

* **NumPy** – numerical calculations and array operations
* **Matplotlib** – plotting and visualization
* **SciPy** – Euclidean distance calculation using `cdist`

Install the required libraries using:

```bash
pip install numpy matplotlib scipy
```

---

## 📂 Project Structure

```text
M-PSK-M-QAM-SER-Simulation/
│
├── modulation_simulation.py
└── README.md
```

Replace `modulation_simulation.py` with the actual filename of your Python program if it is different.

---

# 🔬 Methodology

The simulation is divided into several major stages.

## 1. Constellation Generation

The program generates four modulation schemes:

| Modulation | Number of Symbols | Type |
| ---------- | ----------------: | ---- |
| QPSK       |                 4 | PSK  |
| 8-PSK      |                 8 | PSK  |
| 16-QAM     |                16 | QAM  |
| 64-QAM     |                64 | QAM  |

### PSK

In Phase Shift Keying, the amplitude remains constant while the phase changes.

For example:

* QPSK → 4 different phases
* 8-PSK → 8 different phases

The constellation points are distributed around a circle.

### QAM

Quadrature Amplitude Modulation changes both amplitude and phase.

The program generates:

* 16-QAM
* 64-QAM

These produce square-grid constellation diagrams.

---

# 🔢 2. Gray Coding

The project includes a custom `gray_code()` function.

Gray coding generates a sequence where adjacent values differ by only one bit.

This is useful in digital communication because neighboring constellation symbols can be assigned bit patterns with minimum bit changes.

The generated Gray sequence is used during constellation mapping.

---

# ⚡ 3. Constellation Normalization

Different modulation schemes have different natural average symbol energies.

To make a fair comparison, each constellation is normalized to have:

```text
Average Symbol Energy = 1
```

The program first calculates the average energy:

```python
E_avg_before = np.mean(np.abs(constellation)**2)
```

Then the constellation is normalized using:

```python
normalized_const = constellation / np.sqrt(E_avg_before)
```

The program validates the result by calculating the average energy again.

The output should be approximately:

```text
Average Energy AFTER normalization: 1.0000
```

---

# 📡 4. AWGN Channel

The transmitted symbols are passed through an **Additive White Gaussian Noise (AWGN)** channel.

The received signal can be represented as:

```text
r = s + n
```

where:

* `r` = received symbol
* `s` = transmitted symbol
* `n` = Gaussian noise

The noise level is controlled using SNR.

The simulation uses:

```text
SNR = 0 to 20 dB
```

---

# 📍 5. Minimum-Distance Detection

At the receiver, the noisy received symbols need to be mapped back to the original constellation points.

The project uses **minimum Euclidean distance detection**.

For every received symbol, the distance to every ideal constellation point is calculated.

The closest point is selected as the detected symbol.

Conceptually:

```text
Received Symbol
       ↓
Calculate distance to all constellation points
       ↓
Find minimum distance
       ↓
Detected Symbol
```

The project uses SciPy's:

```python
cdist()
```

function to calculate these distances.

---

# 📊 6. Constellation Visualization

The program generates constellation plots for:

* QPSK
* 8-PSK
* 16-QAM
* 64-QAM

The received symbols are generated using an SNR of **10 dB**.

The plots contain:

* Noisy received symbols
* Ideal constellation points
* I-axis
* Q-axis
* Grid
* Legend

The ideal points are shown using red `x` markers, while the received symbols form noisy clusters around them.

---

# 📈 7. SER Calculation

SER stands for:

> **Symbol Error Rate**

It represents the fraction of transmitted symbols that are detected incorrectly.

The calculation used in the project is:

```text
SER = Number of Symbol Errors / Total Number of Transmitted Symbols
```

For example, if 100 symbols are transmitted and 5 are detected incorrectly:

```text
SER = 5 / 100
    = 0.05
```

The simulation uses:

```python
N_SYMBOLS = 10000
```

for each SNR value.

---

# 📉 8. SER vs SNR

The simulation evaluates the following SNR values:

```text
0, 2, 4, 6, 8, 10, 12, 14, 16, 18, 20 dB
```

For every SNR value:

1. Random symbols are generated.
2. Symbols are transmitted.
3. AWGN is added.
4. Received symbols are detected.
5. Detected symbols are compared with transmitted symbols.
6. SER is calculated.
7. The result is stored.

Finally, the results are plotted as:

```text
SER vs SNR
```

A logarithmic scale is used for SER because error rates can span several orders of magnitude.

---

# 📈 Expected Results

The constellation diagrams should show that increasing noise causes received points to spread around the ideal constellation locations.

At higher SNR:

```text
Less noise
    ↓
Tighter constellation clusters
    ↓
More accurate detection
    ↓
Lower SER
```

At lower SNR:

```text
More noise
    ↓
Greater constellation spreading
    ↓
More detection errors
    ↓
Higher SER
```

Higher-order modulation schemes such as 64-QAM have more closely spaced constellation points than QPSK.

Therefore, noise can cause symbol decisions to cross neighboring decision regions more easily.

---

# 🧪 Simulation Parameters

The main parameters used in the experiment are:

```python
N_SYMBOLS = 10000
```

Number of symbols simulated for each SNR point.

```python
snr_range = np.arange(0, 21, 2)
```

SNR range from 0 dB to 20 dB in 2 dB steps.

For constellation visualization:

```python
snr_test_points = [0, 5, 10, 20]
```

The displayed noisy constellation uses:

```text
10 dB SNR
```

---

# ▶️ How to Run

## Step 1 — Install Python

Install Python 3.x on your computer.

Verify the installation:

```bash
python --version
```

---

## Step 2 — Install Dependencies

Run:

```bash
pip install numpy matplotlib scipy
```

---

## Step 3 — Save the Python Code

Save the simulation code as:

```text
modulation_simulation.py
```

---

## Step 4 — Run the Program

Open a terminal in the project directory and run:

```bash
python modulation_simulation.py
```

The program will:

1. Print constellation energy validation.
2. Display constellation diagrams.
3. Calculate SER values.
4. Display the SER vs SNR graph.

---

# 📋 Example Validation Output

The program prints the average energy before and after normalization.

Example:

```text
--- Mandatory Validation: QPSK ---
Average Energy BEFORE normalization: 1.0000
Average Energy AFTER normalization:  1.0000

--- Mandatory Validation: 8-PSK ---
Average Energy BEFORE normalization: 1.0000
Average Energy AFTER normalization:  1.0000

--- Mandatory Validation: 16-QAM ---
Average Energy BEFORE normalization: 10.0000
Average Energy AFTER normalization:  1.0000

--- Mandatory Validation: 64-QAM ---
Average Energy BEFORE normalization: 42.0000
Average Energy AFTER normalization:  1.0000
```

The exact numerical values can vary depending on the constellation implementation, but the normalized average energy should be approximately **1.0**.

---

# 🧠 Key Concepts Demonstrated

This project demonstrates several important digital communication concepts:

* M-ary modulation
* PSK
* QAM
* Gray coding
* Complex baseband representation
* I/Q components
* Symbol energy
* SNR
* AWGN
* Euclidean distance
* Maximum/nearest-point detection
* Symbol Error Rate
* Constellation diagrams
* Communication-system simulation

---

# 📚 Mathematical Background

## PSK Signal Representation

A PSK constellation can be represented as:

```text
s_k = A e^(jθ_k)
```

where:

* `A` = signal amplitude
* `θ_k` = phase of the kth symbol
* `j` = imaginary unit

For M-PSK:

```text
θ_k = 2πk/M
```

---

## QAM Representation

A QAM symbol can be represented as:

```text
s = I + jQ
```

where:

* `I` = In-phase component
* `Q` = Quadrature component

---

## AWGN Model

The received signal is:

```text
r = s + n
```

where `n` represents additive Gaussian noise.

---

## Symbol Error Rate

```text
SER = N_error / N_total
```

where:

* `N_error` = number of incorrectly detected symbols
* `N_total` = total number of transmitted symbols

---

# 🔍 Important Observation

One of the main observations from this experiment is the trade-off between **spectral efficiency and noise tolerance**.

Higher-order modulation schemes can represent more information per symbol.

For example:

```text
QPSK    → log₂(4)  = 2 bits/symbol
8-PSK   → log₂(8)  = 3 bits/symbol
16-QAM  → log₂(16) = 4 bits/symbol
64-QAM  → log₂(64) = 6 bits/symbol
```

However, increasing the modulation order also increases the number of constellation points, making the points more closely spaced after normalization.

This makes reliable detection more dependent on adequate SNR.

---

# 🚀 Possible Future Improvements

This project can be extended in several ways:

* Add BPSK
* Add 16-PSK
* Add 256-QAM
* Add theoretical SER curves
* Add BER calculation
* Compare Gray mapping with non-Gray mapping
* Add Rayleigh fading
* Add Rician fading
* Add channel coding
* Add pulse-shaping filters
* Add Root Raised Cosine filtering
* Add eye-diagram analysis
* Add Eb/N₀-based simulation
* Create an interactive GUI
* Compare simulated and theoretical performance

---

# 🎓 Applications

The concepts demonstrated in this project are used in modern communication systems such as:

* Wireless communication
* Digital television
* Wi-Fi
* Cellular communication
* Satellite communication
* Microwave communication
* Digital radio
* Modems
* OFDM-based communication systems

---

# 👨‍💻 Author

**Rakesh Karmakar**

Electronics and Communication Engineering

---

## ⭐ Project Summary

This project provides a practical simulation of digital modulation performance using Python.

The complete communication chain is:

```text
Random Symbols
      ↓
Constellation Mapping
      ↓
Energy Normalization
      ↓
AWGN Channel
      ↓
Received Symbols
      ↓
Minimum-Distance Detection
      ↓
Symbol Comparison
      ↓
SER Calculation
      ↓
SER vs SNR
```

---

## 📜 License

This project is intended for educational and academic purposes.
