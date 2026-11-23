# 🌕 MoonAnything

**A Vision Benchmark with Large-Scale Lunar Supervised Data**

*Accepted at ACM MMSys 2026*

[![Dataset DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.18415119.svg)](https://doi.org/10.5281/zenodo.18415119)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

MoonAnything is a large-scale benchmark for computer vision on the lunar surface. It combines **geometric** and **photometric** supervision in two complementary sub-datasets, supporting tasks from stereo matching and 3D reconstruction to monocular depth, normal and reflectance estimation.

MoonAnything extends our earlier datasets [StereoLunar](https://zenodo.org/records/17514376) and [Lunar-G2R](https://zenodo.org/records/17964776).

---

## Overview

| Sub-dataset | Archive | Region | Data | Example tasks |
|---|---|---|---|---|
| **LunarGeo** | `StereoGeo.zip` (11.4 GB) | South Pole, Tycho crater | Stereo image pairs, dense depth maps, camera poses | Stereo matching, multi-view 3D reconstruction, camera pose estimation |
| **LunarPhoto** | `LunarPhoto.zip` (11.0 GB) | Tycho crater | DEM patches, LRO NAC images, SVBRDF / normal / depth / line-of-sight maps, multi-illumination renderings | Monocular depth estimation, photometric-stereo normal estimation, reflectance (BRDF) estimation, illumination-robust learning |

### LunarGeo

- Stereo pairs rendered with a Hapke BRDF, plus an SVBRDF for Tycho
- Three camera motion types: **nadir**, **oblique** and **dynamic**
- Coverage across **10 altitude bands**
- Ground truth: dense depth maps and camera extrinsics

See `readme_geo.txt` on Zenodo for file layout and conventions.

### LunarPhoto

- DEM patches of 128 × 128 px at 5 m/px, paired with LRO NAC images (0.5 to 2 m/px)
- Per-sample SVBRDF, normal, depth and line-of-sight maps
- **9 solar illumination conditions** sampled with SPICE, each rendered with both a Hapke BRDF and the SVBRDF (18 renderings per sample)

---

## Download

The dataset (22.4 GB in total) is hosted on Zenodo: **[doi.org/10.5281/zenodo.18415119](https://doi.org/10.5281/zenodo.18415119)**

```bash
# LunarGeo
wget -O StereoGeo.zip "https://zenodo.org/records/18415119/files/StereoGeo.zip?download=1"

# LunarPhoto
wget -O LunarPhoto.zip "https://zenodo.org/records/18415119/files/LunarPhoto.zip?download=1"
```

Verify the archives after downloading:

```bash
md5sum StereoGeo.zip LunarPhoto.zip
# d645af1a6649c0d93f8e8a454e451b64  StereoGeo.zip
# 3a9fd7200d5ab0e35343719c5133fcff  LunarPhoto.zip
```

---

## Related Work

- **StereoLunar**: C. Grethen et al., *Adapting Stereo Vision From Objects To 3D Lunar Surface Reconstruction*, ICCV 2025 Workshops (3D-VAST). [Paper](https://openaccess.thecvf.com/content/ICCV2025W/3D-VAST/papers/Grethen_Adapting_Stereo_Vision_From_Objects_To_3D_Lunar_Surface_Reconstruction_ICCVW_2025_paper.pdf) · [Data](https://zenodo.org/records/17514376)
- **Lunar-G2R**: [Data](https://zenodo.org/records/17964776)
- **BRDF extraction method**: [arXiv:2601.10449](https://arxiv.org/abs/2601.10449)

---

## Citation

If you use MoonAnything in your research, please cite both the paper and the dataset:

```bibtex
@inproceedings{grethen2026moonanything,
  title     = {MoonAnything: A Vision Benchmark with Large-Scale Lunar Supervised Data},
  author    = {Grethen, Cl{\'e}mentine and Shi, Yuang and Gasparini, Simone and Morin, G{\'e}raldine},
  booktitle = {Proceedings of the ACM Multimedia Systems Conference 2026},
  pages     = {457--463},
  year      = {2026}
}

@misc{grethen2026moonanything_data,
  title     = {MoonAnything: A Vision Benchmark with Large-Scale Lunar Supervised Data},
  author    = {Grethen, Cl{\'e}mentine and Shi, Yuang and Gasparini, Simone and Morin, G{\'e}raldine},
  publisher = {Zenodo},
  version   = {v1},
  year      = {2026},
  doi       = {10.5281/zenodo.18415119},
  url       = {https://doi.org/10.5281/zenodo.18415119}
}
```

---

## License

The MoonAnything dataset is released under the [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/) license.

LRO NAC imagery and DEM data originate from NASA's Lunar Reconnaissance Orbiter mission.
