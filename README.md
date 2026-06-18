# Frequency Mixer and De-Mixer

This repository contains the coursework implementation for **EE200: Signals, Systems and Networks**. The project explores how Fourier-domain methods can be used to manipulate both images and audio:

- **Problem 1: Frequency Mixer - "Beauty and the Blur"**
  Combines the **high-frequency details** of one image with the **low-frequency structure** of another to create a hybrid image.
- **Problem 2: Frequency De-Mixer - "Unwanted Solo"**
  Uses frequency-selective filtering to suppress an unwanted instrumental component from a corrupted music track.

The work is implemented in Python notebooks and supported by a report, generated plots, and output media files.

## Repository Contents

```text
freq_mixer/
|-- Lalit_240591_Q1.ipynb              # Image frequency analysis and fusion
|-- Lalit_240591_Q2.ipynb              # Audio frequency analysis and filtering
|-- EE00_Report_Lalit_240591.pdf       # Detailed report
|-- SignalProcessing_PS.pdf            # Assignment brief
|-- cat_gray.jpg                       # Input image for high-frequency details
|-- dog_gray .jpg                      # Input image for low-frequency structure
|-- song_with_2piccolo .wav            # Corrupted input audio
|-- problem1/                          # Plots and image outputs for Q1
`-- problem2/                          # Plots and audio outputs for Q2
```

## Problem 1: Frequency Mixer

### Objective

Analyze the 2D Fourier transform of grayscale images and create a hybrid image by combining:

- **Low frequencies** from the dog image for overall shape and structure
- **High frequencies** from the cat image for edges and fine texture

### What the notebook does

- Loads and resizes the input images
- Computes the **2D DFT** using `numpy.fft.fft2`
- Visualizes magnitude spectra in normal scale and logarithmic dB scale
- Applies `fftshift` to center low-frequency content
- Rotates an image by 90 degrees and compares its spectrum with the original
- Builds circular **low-pass** and **high-pass** masks
- Reconstructs a fused image using inverse Fourier transform

### Key implementation details

- Libraries used: `numpy`, `matplotlib`, `Pillow`
- Circular mask radius used for fusion: approximately `14`
- Weighted fusion used in the notebook with low-frequency contribution `0.9` and high-frequency contribution `0.7`

### Outputs

Generated outputs for this part are stored in [`problem1/`](./problem1), including:

- frequency analysis plots for both images
- centered spectra
- rotated-spectrum comparison
- difference spectrum
- low-pass and high-pass mask visualizations
- final fused image

## Problem 2: Frequency De-Mixer

### Objective

Analyze a corrupted audio signal and remove an unwanted solo instrumental component using frequency-domain filtering.

### What the notebook does

- Loads the input `.wav` file
- Visualizes the waveform and spectral content
- Inspects dominant frequency regions using magnitude spectrum, spectrogram, and power spectral density
- Designs FIR filters with `scipy.signal.firwin`
- Compares low-pass, high-pass, and band-stop filtering strategies
- Exports filtered audio signals for evaluation

### Key implementation details

- Libraries used: `numpy`, `matplotlib`, `librosa`, `soundfile`, `scipy`
- FIR filter window: `Blackman`
- Number of taps: `1001`
- Frequency ranges explored in the notebook include a low-pass cutoff near `1050-1150 Hz`, a high-pass cutoff near `6000 Hz`, and a band-stop region near `1050-6000 Hz`

### Outputs

Generated outputs for this part are stored in [`problem2/`](./problem2), including:

- waveform and filter-response plots
- filtered audio versions (`lowpass.wav`, `highpass.wav`, `bandstop.wav`)
- final processed result audio

## Results Summary

### Image mixing

The hybrid-image experiment demonstrates the perceptual role of spatial frequencies:

- low frequencies preserve coarse structure
- high frequencies preserve local detail
- rotating an image rotates its frequency-domain representation accordingly

### Audio filtering

The audio experiment shows how unwanted components can be isolated by their spectral footprint and attenuated with carefully chosen FIR filters. The notebook evaluates multiple filter types before producing a cleaned result.

## How to Run

### Requirements

Install the required Python packages:

```bash
pip install numpy matplotlib pillow librosa soundfile scipy
```

### Running the notebooks

Open and run:

```bash
Lalit_240591_Q1.ipynb
Lalit_240591_Q2.ipynb
```

If you are running the notebooks locally instead of Google Colab, you may need to update any hardcoded `/content/...` file paths to match your local folder structure.

## Report

The full explanation, observations, plots, and discussion are available in [`EE00_Report_Lalit_240591.pdf`](./EE00_Report_Lalit_240591.pdf).

## Author

**Lalit Meena**  
Roll No.: `240591`  
Course: `EE200 - Signals, Systems and Networks`
