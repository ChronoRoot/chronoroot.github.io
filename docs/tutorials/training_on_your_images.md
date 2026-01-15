# Annotation & Training Tutorial

## 1. Data Pipeline: From Raw Video to Annotation Ready

Before manual refinement begins, we leverage the existing model and temporal consistency to generate high-quality "silver standard" labels. This ensures biologists never start from a blank canvas.

### Step A: Temporal Segmentation & Inference

1. **Full Video Inference:** Run the `nnU-Net` model on the **complete video sequence** with temporal post-processing enabled. This produces initial segmentation masks for every frame in the video.
2. **Format Conversion:** Run the script in `segmentationApp/trainerOrganization` to convert these outputs into **`.nii.gz`** (NIfTI) files. This format is compatible with ITK-SNAP for manual refinement and allow us to have the same naming convention between images and labels.

### Step B: Expert Frame Selection & Organization

Frame selection is a manual, expert-driven process. You must browse the processed videos to identify frames that provide the highest educational value for the model.

1. **Growth Stage Coverage:** Select frames across the entire timeline—from the first signs of germination to complex, late-stage root architectures.
2. **Failure Analysis:** Identify "failure frames" where artifacts (plate edges, condensation, or agar bubbles) caused the model to produce errors.
3. **Folder Hierarchy:** Manually check the predictions pairs are in the correct structure:

`[Species]Dataset/[Experiment_Type]/[Robot_ID]/[Camera_ID]/[Filename]`

---

## 2. Data Organization & Experimental Design

Understanding the hierarchy is essential for the training scripts to correctly associate images with their biological context. Correct folder structure examples are provided in the HuggingFace training dataset.

### Folder Hierarchy

* **Arabidopsis:** `ArabidopsisDataset/[Experiment_Type]/[Robot_ID]/[Camera_ID]/[Filename]`
* **Tomato:** `TomatoDataset/[Robot_ID]/[Camera_ID]/[Filename]` (omits the experiment type subfolder).

**Experiment Types (Arabidopsis):**

* **Roots:** Standard root analysis (up to 2 weeks) including lateral root development.
* **Germination:** Focus on the moment of radicle emergence (typically the first 3 days).
* **Etiolation:** Hypocotyl elongation studies conducted in dark conditions.
* **ManyRoots:** Multiple plants per plate, but tracking only the primary root for one week.

**Metadata IDs:**

* **Robot ID:** The Raspberry Pi module number, followed by the experiment timestamp (`rpiXX_YYYY-MM-DD_HH-MM`).
* **Camera ID:** Numbers 1 to 4, representing the physical position from left to right.

---

## 3. Our Sampling Strategy by Experiment

We do not annotate every frame. We combine biological milestones with model qualitative performance:

| Experiment | Biological Focus | Typical Sampling |
| --- | --- | --- |
| **Root Analysis** | Architecture & branching | 5–8 images (from early to late stages) |
| **Germination** | Radicle emergence | 2–3 images (seed, some germinated, fully germinated) |
| **Etiolation** | Hypocotyl elongation | 3–4 images |
| **ManyRoots** | Primary root tracking | 4–6 images (over first week) |
| **Tomato** | Architecture | 5–8 images |

Always prioritize frames where the model fails. The worse the model performs, the more valuable that frame is for the next training iteration.

---

## 4. Manual Annotation Protocol (ITK-SNAP)

ITK-SNAP handles NIfTI files, allowing us to store all plant organ classifications in a single file.

### Initial Setup

1. **Load Main Image:** Drag the `.png` into the window  Select **"Generic ITK Image"**.
2. **Load Segmentation:** Drag the `.nii.gz` prediction  Select **"Segmentation Image"**.
3. **Optimize View:** Click the **2D-only layout button** (the single square icon in the bottom right corner).

### The Biologist's Label Map

Accuracy is vital. A "Stem" labeled as "Primary Root" will confuse the model’s morphological understanding.

| ID | Label Name | Color | Biological Definition |
| --- | --- | --- | --- |
| **0** | **Background** | Clear | Agar, plate edges, condensation, noise. |
| **1** | **Primary Root** | Red | The main root axis originating from the seed. |
| **2** | **Lateral Roots** | Green | All secondary or tertiary branching roots. |
| **3** | **Seed** | Blue | The seed coat or the initial grain. |
| **4** | **Stem** | Yellow | **Hypocotyl**. The transition between root and leaves. |
| **5** | **Leaves** | Cyan | For Tomato: Includes the **Petioles** (Aerial Part). |
| **6** | **Petioles** | Pink | **Arabidopsis only**: The leaf stalks. |

### Annotation Controls & Tips

* **Brush Shape:** Always use the **Round Brush** for natural plant structures.
* **Navigation:** Select the **Magnifying Glass**.
* *Zoom:* Hold **Right-Click** and drag.
* *Pan:* **Left-Click** and drag.


* **The "Paint Over" Rule:** To fix a misclassification (e.g., changing a model-predicted Primary Root to a Lateral Root):
1. Select the correct Active Label (e.g., Green/Lateral).
2. Set the tool to **"Paint Over Label"** mode.
3. Select the incorrect label (e.g., Red/Primary) in the "Over" dropdown.
4. This ensures you only edit the specific pixels needing correction without bleeding into the background.



---

## 5. Understanding nnU-Net v2 Data Organization

nnU-Net v2 requires a specific environment and directory structure. It relies on three main environment variables you must set in your system:

* `nnUNet_raw`: Where you place your raw datasets (images and labels).
* `nnUNet_preprocessed`: Where the framework saves cropped, resampled, and normalized data.
* `nnUNet_results`: Where the trained model weights and logs are stored.

### The Raw Dataset Structure

Every dataset must follow the naming convention `DatasetXXX_Name` (e.g., `Dataset001_Tomato`). Inside that folder, you must have:

* **`imagesTr/`**: Training images named as `{CASE_ID}_0000.nii.gz`.
* **`labelsTr/`**: Training labels named as `{CASE_ID}.nii.gz`.
* **`dataset.json`**: The metadata file.

---

## 6. Training Preparation

### Step 1: Format Conversion & Aggregation

Navigate to `segmentationApp/trainerOrganization` in the ChronoRoot2 Repository. Use the provided notebooks to:

1. Aggregate your expert-selected `Robot/Camera` folders.
2. Automatically rename them to the `{CASE_ID}_0000.nii.gz` format required by nnU-Net.
3. Move them into the `imagesTr` and `labelsTr` folders.

### Step 2: The `dataset.json`

You must manually prepare this file in the `nnUNet_raw/DatasetXXX/` folder.

* **Tomato:** Copy `dataset_tomato.json` from the repository.
* **Arabidopsis:** Copy `dataset_arabidopsis.json` from the repository.
* **Action:** Rename the copy to `dataset.json` and update the `numTraining` field to match your actual number of training cases.

### Step 3: Data Splitting (Anti-Leakage)

To prevent "overfitting" where the model recognizes specific plate geometry:

1. The notebook groups images by their `Robot/Camera` ID so frames from the same video are never split between training and validation.
2. It generates a `splits_final.json`.
3. **Manual Step:** You must copy this file to `nnUNet_preprocessed/DatasetXXX/splits_final.json` before training starts.

---

## 7. Execution & Commands

Once organized, run the following in your terminal:

1. **Plan & Preprocess:**
This extracts the "fingerprint" of your data (intensities, sizes) and prepares the files.

```bash
nnUNetv2_plan_and_preprocess -d [DATASET_ID] -c 2d

```

2. **Train (5-Fold Cross-Validation):**
Run this for folds 0 through 4 to complete the ensemble.

```bash
nnUNetv2_train [DATASET_ID] 2d [FOLD_NUMBER]

```

---

## 8. Useful Resources

* [nnU-Net v2 Official Documentation](https://github.com/MIC-DKFZ/nnUNet): Detailed guide on data formats and environment variables.
* [Locations of Scripts in ChronoRoot2 Repository](https://github.com/ChronoRoot/ChronoRoot2/tree/master/segmentationApp/trainerOrganization): Access the trainer scripts and `dataset.json` templates.
* [ITK-SNAP Official Site](http://www.itksnap.org/): Documentation for advanced segmentation tools.
