Please see the relevant issue [here](https://github.com/bids-standard/bep001/issues/9).

## Classification of the suggested metadata fields 

The RECOMMENDED metadata fields in the main spec are divided into 8 classes. Suggested metadata fields ([#9](https://github.com/bids-standard/bep001/issues/9)) are planned to be inserted under corresponding categories as follows:  

* Scanner hardware 
* Sequence specifics 
    * SpoilingRFPhaseIncrement 
    * SpoilingGradientMoment
    * SpoilingGradientDuration 
    * MagnetizationTransfer 
    * MTPulseShape
    * MTPulseBandwidth
    * MTOffsetFrequency
* In-plane spatial encoding
* Timing parameters 
     * Mixing Time 
* RF & Contrast 
* Slice acceleration 
* Anatomical landmarks 
* Institution information 

## Descriptions of the suggested metadata fields 

### Spoiling and magnetization transfer related fields 

The terms defined by `Sequence variant` DICOM attribute [(0018,0021)](http://dicomlookup.com/lookup.asp?sw=Tnumber&q=(0018,0021)) can be of help to populate _spoiling_ and _magnetization transfer_ related fields. The terms defined by 0018, 0021 are as follows: 

* `SK`: Segmented k-space
* `MTC`: Magnerization transfer contrast 
* `SS`: Steady state 
* `TRSS`: Time-reversed steady state 
* `SP`: Spoiled 
* `MP`: Magnetization prepared 
* `OSP`: Oversampling phase
* `NONE`: No sequence variant 

For example, `Sequence Variant` DICOM tag equals to `MTC\SP` for a product FLASH sequence for which magnetizatoin transfer option is enabled. This case typically corresponds to the `MTon` label of the `-acq` key-value pair for `MTR`, `MTS` or `MPM`. When the magnetization transfer is not applied - `MToff` or `T1w` - the `Sequence Variant` DICOM tag equals to `SP`. 

#### Magnetization transfer

| Field Name        | Definition                                                                                                                                                                                                                                                                                              |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| MTState           | RECOMMENDED. Boolean value (`true` or `false`), specifying whether the magnetization transfer pulse is applied. This parameter is REQUIRED by all the anatomical images grouped by `MTR`, `MTS` and `MPM` suffixes. This field originally corresponds to DICOM tag 0018, 9020 `Magnetization Transfer`. |
| MTOffsetFrequency | RECOMMENDED. The frequency offset of the magnetization transfer pulse with respect to the central H1 Larmor frequency in Hertz (Hz).                                                                                                                                                                    |
| MTPulseBandwidth  | RECOMMENDED. The excitation bandwidth of the magnetization transfer pulse in Hertz (Hz).                                                                                                                                                                                                                |
| MTNumberOfPulses  | RECOMMENDED. Number of magnetization transfer RF pulses applied before the readout.                                                                                                                                                                                                                     |
| MTPulseShape      | RECOMMENDED. Shape of the magnetization transfer RF pulse waveform. Accepted values: `HARD`, `GAUSSIAN`, `GAUSSHANN` (gaussian pulse with Hanning window), `SINC`, `SINCHANN` (sinc pulse with Hanning window), `SINCGAUSS` (sinc pulse with Gaussian window), `FERMI`.                                 |
| MTPulseDuration   | RECOMMENDED. Duration of the magnetization transfer RF pulse in seconds.                                                                                                                                                                                                                                |   

#### Spoiling

| Field Name               | Definition                                                                                                                                                                                |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SpoilingState            | RECOMMENDED. Boolean value (`true` or `false`), specifying whether the pulse sequence uses any type of spoiling stratey to suppress transverse magnetization remaining after the readout. |
| SpoilingType             | RECOMMENDED. Specifies which spoiling method(s) are used by a spoiled sequence. Accepted values: `RF`, `GRADIENT` or `COMBINED`.                                                          |
| SpoilingRFPhaseIncrement | RECOMMENDED. The amount of incrementation described in degrees, which is applied to the phase of the excitation pulse at each TR period for achieving RF spoiling.                        |
| SpoilingGradientMoment   | RECOMMENDED. Zeroth moment of the spoiler gradient lobe in militesla times second per meter (mT.s/m).                                                                                     |
| SpoilingGradientDuration | RECOMMENDED. The duration of the spoiler gradient lobe in seconds. The duration of a trapezoidal lobe is defined as the summation of ramp-up and plateu times.                            |