# 🌕 MoonAnything

**A Vision Benchmark with Large-Scale Lunar Supervised Data**

*Accepted at ACM MMSys 2026*

[![Dataset DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.18415119.svg)](https://zenodo.org/records/23534735)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

MoonAnything is a large-scale benchmark for computer vision on the lunar surface. It combines **geometric** and **photometric** supervision in two complementary sub-datasets, supporting tasks from stereo matching and 3D reconstruction to monocular depth, normal and reflectance estimation.

MoonAnything extends our earlier datasets [StereoLunar](https://zenodo.org/records/23534735) and [Lunar-G2R](https://zenodo.org/records/23534735).

---

## Overview

| Sub-dataset | Archive(s) | Region | Data | Example tasks |
|---|---|---|---|---|
| **LunarGeo** | `StereoGeo.zip.part00`–`part04` (~51 GB, reassemble with `cat`) | South Pole, Tycho crater | Stereo image pairs, dense depth maps, camera poses | Stereo matching, multi-view 3D reconstruction, camera pose estimation |
| **LunarPhoto** | 13 independent files at the record root (~141 GB; `brdf_map`, `normal_map` and `multilighting_hapke_rendering` are split into parts) | Tycho crater | DEM patches, real LRO NAC images, BRDF / normal / depth / line-of-sight maps, multi-illumination renderings (Hapke and learnt SVBRDF) | Monocular depth estimation, photometric-stereo normal estimation, reflectance (BRDF) estimation, illumination-robust learning |

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

The dataset (~199 GB in total) is hosted on Zenodo: **[zenodo.org/records/23534735](https://zenodo.org/records/23534735)**

```bash
BASE="https://zenodo.org/records/23534735/files"

# LunarGeo (StereoGeo, 5 parts, ~51 GB)
for p in 00 01 02 03 04; do
  wget -c -O StereoGeo.zip.part$p "$BASE/StereoGeo.zip.part$p?download=1"
done
cat StereoGeo.zip.part* > StereoGeo.zip && unzip StereoGeo.zip

# LunarPhoto (~148 GB) — download only the modalities you need
for f in README.md train_dataset.csv val_dataset.csv tst_dataset.csv \
         render.zip dem.zip metadata.zip depth_map.zip los_map.zip \
         multilighting_SVBRDF_rendering.zip \
         brdf_map.zip.part0{0,1} normal_map.zip.part0{0,1} \
         multilighting_hapke_rendering.zip.part0{0,1,2,3,4}; do
  wget -c -O "$f" "$BASE/$f?download=1"
done

# Reassemble split archives
for n in brdf_map normal_map multilighting_hapke_rendering; do
  cat $n.zip.part* > $n.zip
done
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
  doi       = {10.5281/zenodo.23534735},
  url       = {https://doi.org/10.5281/zenodo.23534735}
}
```

---

## License

The MoonAnything dataset is released under the [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/) license.

LRO NAC imagery and DEM data originate from NASA's Lunar Reconnaissance Orbiter mission.
