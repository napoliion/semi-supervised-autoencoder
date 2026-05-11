# Semi-supervised autoencoders (s2ae) for xenon TPCs

This is a proof-of-concept for a semi-supervised autoencoder (AE) which compresses spatial or temporal data with a partially physically interpretable latent space representation. Xenon dual-phase time projection chambers measure light produced from particle interactions using arrays of photosensors. This light data can be represented either spatially or temporally: each photosensor reads out time-series data of waveform signals, and these individual waveforms can be integrated over time in which the total amount of light seen per photosensor in an array is termed a hit pattern. 

This AE was specifically designed to work with ionization signals (commonly referred to as S2 signals in the xenon dual-phase TPC community) which are generated from drifted ionization electrons, since the goal is to simultaneously compress a hit pattern or a given photosensor waveform while simultaneously inferring the number of ionization electrons in the latent space.

The semi-supervised nature of the AE comes from the fact that part of the latent space is supervised, as several values in the latent space vector are constrained through a loss function penalty while the rest of the values are free to evolve unsupervised. The loss function includes three terms, two of which penalize incorrectly inferred numbers of ionization electrons and (x,y) S2 positions, and a third which penalizes incorrectly reconstructed data when comparing the input and output.

## Publication

The proceeding established the proof-of-concept:

> **Energy Reconstruction with Semi-Supervised Autoencoders for Dual-Phase Time Projection Chambers**
> Ivy Li, Aarón Higuera, Shixiao Liang, Juehang Qin, Christopher Tunnell (2024)
> [EPJ Web of Conferences 295, 09022](https://doi.org/10.1051/epjconf/202429509022) — CHEP 2023

Additional work was conducted after the proceeding for my thesis including model testing on time-series data and several architectural changes.

## Status

Code is being refactored from notebooks.  Ongoing work on the temporal model.

## Data

The spatial AE takes in a hit pattern of 494 photosensors, but this can be changed as the dimensions of the autoencoder input just needs to match the number of photosensors. This was tested on both normalized and raw data. The temporal AE takes in 200 samples as XENONnT typically downsamples its longer S2 waveforms such that each S2 signal fits within 200 samples. 

## Results and Discussion

In testing possible latent space dimensions (i.e. how much can you compress?) we found the optimal performance to be a latent vector of 10 values. Lower latent space dimensions would occasionally cause the AE to hallucinate additional signals in the reconstructed hit pattern. In both the spatial and temporal AE cases, we have found that the inferred number of ionization electrons shows strong agreement with the simulated ground truth along the expected energy range.

Future work on this project includes further development on spatiotemporal data, as the compression would be the most impactful in raw waveform data without downsampling, which would result in sparse spatiotemporal arrays. 

## Citation

If referencing this work, please cite with the following BibTeX:

```
@article{Li:2024fnw,
    author = "Li, Ivy and Higuera, Aar{\'o}n and Liang, Shixiao and Qin, Juehang and Tunnell, Christopher",
    title = "{Energy Reconstruction with Semi-Supervised Autoencoders for Dual-Phase Time Projection Chambers}",
    doi = "10.1051/epjconf/202429509022",
    journal = "EPJ Web Conf.",
    volume = "295",
    pages = "09022",
    year = "2024"
}
```

## License

MIT License.
