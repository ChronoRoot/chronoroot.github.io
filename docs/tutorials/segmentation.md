## Graphical User Interface (GUI) Usage

To begin the segmentation process, launch the segmentation interface. This will open the main segmentation window.

![Segmentation Interface Main Window](segmentation_images/0.png)

The interface contains only a few buttons:

* **Load Robot:** Imports data from a Raspberry Pi module, including time series data from all four hardware module cameras
* **Conda:** Specifies the Anaconda environment name (leave unchanged if using Docker or installing by Conda .yml)
* **Alpha:** Defined for weighted average trailing in post-processing.
* **Species selector:** defines which model weights to load, as stored in the models folder.
* **Fast Mode:** won’t perform test-time augmentation if selected. 3x speed increase at the cost of a small loss in performance.

**Load Your Data:** 

Begin by loading all robot datasets individually from the demo folder. In this demonstration, each robot contains data from one camera, with three robots total corresponding to each experiment.

![Segmentation Interface Load Robot](segmentation_images/1.png)

**Queue Your Jobs and Monitor Progress:** 

Add all robot folders to the processing queue. You'll notice the status indicator will update to either "Processing" or "Queued" depending on the current workload. The log panel at the bottom displays important process information and updates. Allow the complete segmentation process to finish before proceeding to the next step.

![Segmentation Interface Loaded Images](segmentation_images/2.png)
![Segmentation Interface Queue](segmentation_images/3.png)
![Segmentation Interface Queue progress](segmentation_images/4.png)

---

## Command Line Interface (CLI) Usage

If you prefer working in a headless environment, automating tasks, or simply wish to avoid the graphical interface, you can perform segmentation directly via the command line.

**Prerequisites:**
Before running the commands below, ensure you have loaded the `ChronoRoot` environment.

### Basic Usage

The basic syntax requires pointing the script to your input folder (equivalent to "Load Robot" in the GUI).

```bash
python cli_interface.py /path/to/your/images

```

### Common Examples

**1. Standard Arabidopsis Segmentation**
Runs the default segmentation for Arabidopsis using the GPU.

```bash
python cli_interface.py /path/to/dataset --species arabidopsis

```

**2. Tomato Segmentation in Fast Mode**
Use this for Tomato datasets if you want faster results (skips test-time augmentation).

```bash
python cli_interface.py /path/to/dataset --species tomato --fast

```

**3. Custom Post-processing**
If you need to adjust the **Alpha** parameter (weighted average trailing) specifically for your dataset:

```bash
python cli_interface.py /path/to/dataset --species arabidopsis --alpha 0.90

```

### Argument Reference

| Argument | Description | GUI Equivalent |
| --- | --- | --- |
| `input` | **Required.** Path to the folder containing images. | "Load Robot" |
| `--species` | Choose between `arabidopsis` (default) or `tomato`. | "Species selector" |
| `--fast` | Disables test-time augmentation for 3x speed (slight performance cost). | "Fast Mode" |
| `--alpha` | Set the alpha parameter for post-processing logic. | "Alpha" |
| `--device` | Specify hardware: `cuda` (default), `cpu`, or `mps`. | N/A |
| `--postprocess-only` | Skip segmentation and rerun post-processing on existing results. | N/A |

### Output Structure

The CLI will create a `Segmentation` folder inside your input directory, organizing results exactly as the GUI does:
`input_path/Segmentation/Fold_0`



