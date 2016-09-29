29.09.2016, Pawel [alxd](https://alxd.org/) Chojnacki and Ryszard Cetnarski

# NeuroOn Hypnogram Analysis

Following my principles of Open Access and Open Notebook Science I'd like to present you my comparative analysis of NeuroOn and a professional polisomnograph recording from two nights. To learn more about the experiment itself, please head back to my [previous blog post](https://alxd.org/neuroon-analysis-sources.html).

## Signal formats

Raw signals are available for download [here](https://alxd.org/data/neuroon-signals-raw.7z), with md5sum `f5c4330e1228f8a3f0bd11bffbfa55ad`.

HDF files for faster access are available for download [here](https://alxd.org/data/neuroon-signals-hdf.7z), with md5sum `288968b276f2a70ea858c6d084c9a5fa`. They were generated using [parse_signal.py](./parse_signal.py).

NeuroOn signal was obtained by using proprietary Intelclinic's scripts I am not allowed to share. They produced four CSV files, containing respectively:

 - EEG signal (125 Hz)
 - accelerometer signal
 - LED activity
 - Staging ([hypnogram](https://en.wikipedia.org/wiki/Hypnogram))

AURA PSG signal was exported to an EDF format using Grass Technologies PSG TWin 4.5.4 and 4.5.2 to minimize the risk of software-derived artifacts. The channels signals include:

 - EOG1-A1
 - EOG2-A1
 - CHIN1-CHIN2
 - CHIN2-CHIN3
 - F3-A2
 - C3-A2
 - O1-A2
 - F4-A1
 - C4-A1
 - O2-A1
 - SNORE (first night only)
 - FLOW (first night only)
 - CHEST (first night only)
 - ABDOMEN (first night only)
 - ECG (first night only)
 - SaO2 (blood oxygen saturation, first night only)
 - HR (heart rate, first night only)
 - LEG1 (first night only)
 - LEG2 (first night only)
 - Pos (first night only)

PSG signals from both nights were scored by a professional and exported to XLS and CSV files.

## Analysis

This is a peer-review version of the analysis (currently) with no clear conclusions or discussion section. Please refrain yourself from making hasty assumptions related to NeuroOn product before it is read and commented by third party researchers. We would like to discuss the science behind the research, not the market viability of the device examined.

The goal of the experiment is to detect time shift between NeuroOn and Aura PSG, each of which use different clock and compare synchronized hypnograms. In order to test NeuroOn's accuracy it is assumed that PSG signal is a source of truth.

[Time_synchronization](./Time_synchronization.ipynb) is the first notebook analyzing time shifts between NeuroOn and PSG signals and hypnograms.

[Hipnogram_comparison](./Hipnogram_comparison.ipynb) uses Cohen's cappa to measure NeuroOn's accuracy compared to the PSG.

[Correlation_test](./Correlation test.ipynb) analyzes different possible methods of correlation between EEG signals, including [previous one](https://github.com/pawelchojnacki/neuroon-notebook) used by Pawel Chojnacki.

[Spectral_analysis](Spectral analysis.ipynb) compares PSG's and NeuroOn's ability to use delta power to determine sleep stages.

The analysis doesn't include research in NeuroOn's use of accelerometer, focusing on EEG stage detection only. Continuing in this direction (especially given additional signal gathered from the bicep) may grant additional insight into NeuroOn's functioning.

## Notebook setup

It is strongly advised to use `virtualenv` for freezing specific version of Python libraries. Please use `pip 8.12` . Instructions:

 - Create `virtualenv` ([what is it?](http://docs.python-guide.org/en/latest/dev/virtualenvs/)) in core project folder and activate it.
 - Run `pip install -r requirements.txt` to install all dependencies. It may be required to update your package installer with `pip install --upgrade pip`.
 - Download [hdf files](https://alxd.org/data/neuroon-signals-hdf.7z) and unzip them to populate the `parsed_data` catalog.
 - Download [raw signal files](https://alxd.org/data/neuroon-signals-raw.7z) and unzip them to populate the `neuroon_signals` catalog.
 - Run `jupyter notebook` to start the notebook.

## All feedback welcome

Feel free to [contact me](mailto:alxd(AT)alxd(DOT)org), fork and share this repository!
