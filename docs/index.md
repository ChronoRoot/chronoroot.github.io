# ChronoRoot 2.0

![Figure](images/mainFigure.png)

<p align="center">
  <a href="http://arxiv.org/abs/2504.14736"><img src="https://img.shields.io/badge/arXiv-2504.14736-red.svg" alt="DOI"></a>
  <a href="https://github.com/ChronoRoot/ChronoRoot2/blob/main/LICENSE"><img src="https://img.shields.io/github/license/ChronoRoot/ChronoRoot2" alt="License"></a>
  <a href="https://hub.docker.com/r/ngaggion/chronoroot"><img src="https://img.shields.io/docker/pulls/ngaggion/chronoroot.svg" alt="Docker"></a>
</p>


**ChronoRoot 2.0** is a comprehensive, open-source solution that merges affordable hardware with state-of-the-art Deep Learning to automate the tracking and analysis of plant development. It includes three specialized graphical interfaces. On Linux and Windows (WSL2), these are installed with custom desktop launchers for a point-and-click experience.

| Icon | Application | Purpose & Capabilities | Tutorials |
| --- | --- | --- | --- |
| <img src="images/logo_seg.ico" width="48"> | **Segmentation App** | **Multi-class segmentation tool:** Uses the nnU-Net engine to segment 6 plant organs. | [Segmentation Guide](tutorials/segmentation.md) - [Training Guide](tutorials/training_on_your_images.md) |
| <img src="images/logo.ico" width="48"> | **Standard Interface** | **Detailed RSA Analysis:** Graph-based analysis of individual plants. Measures growth speeds, gravitropic angles, and different RSA metrics. | [Arabidopsis Guide](tutorials/standard.md) - [Tomato Guide](tutorials/standard_tomato.md) |
| <img src="images/logo_screening.ico" width="48"> | **Screening Interface** | **High-throughput screening:** Automated tracking for up to 100 seeds/plate. Optimized for germination and etiolation studies. | [Germination Guide](tutorials/screening_germination.md) - [Etiolation Guide](tutorials/screening_hypocotyl.md) |

!!! info "Choosing your workflow"
    All experiments begin in the **Segmentation App** to generate segmentation masks. From there, choose the **Standard Interface** if you require detailed root architecture (4-6 plants/plate) or the **Screening Interface** for high-density populations (up to 100 seeds/plate).

---

### Latest News & Major Updates

- **07 Jan 2026:** Added desktop shortcut support for Windows users (via WSL2).
- **15 Dec 2025:** Updated desktop launchers with custom ChronoRoot icons.
- **11 Dec 2025:** Introduced **Apptainer** as the primary installer to support HPC clusters. Docker is now reserved for Mac or advanced users.
- **08 Nov 2025:** Unified the repository into a **single Conda environment** for simplified maintenance and setup.
- **30 Oct 2025:** **nnUNetv2 Port:**
    - Models are now included directly in the repo.
    - Added a new CLI and removed the dependency on the custom nnUNet fork; models now load directly via PyTorch.
    - New model weights are available for *Arabidopsis thaliana* and Tomato multi-class segmentation.
- **20 Apr 2025:** 🚀 **ChronoRoot 2.0 Released!** Featuring a revamped segmentation engine, enhanced analysis modules, and improved UX.
  
--- 

### Training Dataset Changelog

All updates refer to the [ChronoRoot Dataset on HuggingFace](https://huggingface.co/datasets/ngaggion/ChronoRoot2).

- **07 Nov 2025:** Added 48 *Arabidopsis thaliana* images (hypocotyl etiolation), bringing the species total to 913.
- **30 Oct 2025:** Major expansion and restructuring:
    - Added 480 *Solanum lycopersicum* (tomato) images with multi-class masks.
    - Added 170 *Arabidopsis thaliana* images (for germination and multiple plants root analysis), totaling 863.
    - Reorganized directory structure to match biologist annotation folders.
    - Removed legacy nnUNet checkpoints to optimize storage following the ChronoRoot 2.0 deployment.
- **30 Jan 2025:** Converted 526 existing masks from binary to multi-class. Added 167 new images (germination and etiolation), totaling 693.
- **30 Apr 2024:** Initial release of 526 *Arabidopsis thaliana* root images with binary segmentation masks.

---

## Installation

Choose the method that best fits your setup. Native and Apptainer installations provide three desktop shortcuts for ease of use.

=== "Native / Conda (Recommended)"
    *Best for: Linux or Windows WSL where you want desktop integration.*

    **Ubuntu / Linux:**
    ```bash
    wget https://raw.githubusercontent.com/chronoroot/ChronoRoot2/master/installer_conda_linux.sh
    bash installer_conda_linux.sh
    ```

    **Windows (via WSL2):**
    ```bash
    wget https://raw.githubusercontent.com/chronoroot/ChronoRoot2/master/installer_conda_wsl.sh
    bash installer_conda_wsl.sh
    ```

=== "Apptainer / Singularity"
    *Best for: HPC Clusters or single-file container users.*

    **Linux:**
    ```bash
    wget https://raw.githubusercontent.com/chronoroot/ChronoRoot2/master/apptainerInstaller/installer_linux.sh
    bash installer_linux.sh
    ```

    **Windows (via WSL2):**
    ```bash
    wget https://raw.githubusercontent.com/chronoroot/ChronoRoot2/master/apptainerInstaller/installer_windows.sh
    bash installer_windows.sh
    ```

=== "Docker"
    *Best for: macOS users or advanced sandbox environments.*

    ```bash
    docker pull ngaggion/chronoroot:latest
    ```
    *See the [Docker Guide](tutorials/docker.md) for full run commands.*

!!! info "System Requirements"
    - **RAM:** 8 GB min (16 GB recommended)
    - **GPU:** NVIDIA GPU with CUDA 11.0+ (Highly recommended for Segmentation)
    - **macOS Note:** Native installation is not supported; use Docker.

---

## Demo Data and Tutorials

New to ChronoRoot? Download our [Demo Data Videos](https://drive.google.com/drive/folders/1PJCn_MMHcM9KPgz8dYe1F2Cvdt43FS3Z?usp=sharing) and follow these guides to process your first dataset:

- [**Root Analysis** – *Arabidopsis thaliana* (Standard Interface)](tutorials/standard.md)
- [**Root Analysis** – Tomato (Standard Interface)](tutorials/standard_tomato.md)
- [**Germination Analysis** –  *Arabidopsis thaliana* (Screening Interface)](tutorials/screening_germination.md)
- [**Hypocotyl Etiolation Analysis** – *Arabidopsis thaliana* (Screening Interface)](tutorials/screening_hypocotyl.md)

---

## Citation

If you use ChronoRoot 2.0 in your research, please cite our work:

```bibtex
@article{gaggion2025chronoroot,
  title={ChronoRoot 2.0: An Open AI-Powered Platform for 2D Temporal Plant Phenotyping},
  author={Gaggion, Nicolás and others},
  journal={arXiv preprint arXiv:2504.14736},
  year={2025}
}
```

---

## Centralized Resources

* :fontawesome-brands-github: **Software Repository:** [https://github.com/ChronoRoot/ChronoRoot2](https://github.com/ChronoRoot/ChronoRoot2)
* :fontawesome-brands-github-alt: **Hardware Module:** [https://github.com/ChronoRoot/ChronoRootModuleHardware](https://github.com/ChronoRoot/ChronoRootModuleHardware)
* :fontawesome-brands-python: **Module Control:** [https://github.com/ChronoRoot/ChronoRootControl](https://github.com/ChronoRoot/ChronoRootControl)
* :fontawesome-solid-database: **Training Dataset:** [https://huggingface.co/datasets/ngaggion/ChronoRoot2](https://huggingface.co/datasets/ngaggion/ChronoRoot2)
* :material-google-drive: **Demo Data:** [https://drive.google.com/drive/folders/1PJCn_MMHcM9KPgz8dYe1F2Cvdt43FS3Z?usp=sharing](https://drive.google.com/drive/folders/1PJCn_MMHcM9KPgz8dYe1F2Cvdt43FS3Z?usp=sharing)

---
