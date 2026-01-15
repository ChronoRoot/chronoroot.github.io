# Germination Analysis – Arabidopsis thaliana (Screening Interface)

![Screening Interface](screening_images/screening_interface.png)

---

## Interface Components

* **Project Directory:** Specifies the storage location for your analysis results. A project encompasses a complete experimental setup involving one or more Raspberry Pi modules.
* **Video Directory:** Identifies the video file for current processing. Videos must be processed sequentially, one at a time.
* **Analysis Identifier:** Identifies the current plate being analyzed.
* **Time Between Slices:** Sets the temporal resolution of the Raspberry Pi module.
* **Extra Time Before First Picture:** Accounts for additional time lost when plates are removed from cold storage or placed under light conditions, ensuring accurate germination timing calculations.
* **End germination plot time (hours):** Specifies the cutoff time for germination analysis.
* **Calibration Settings:** Converts measurements from pixels to millimeters for accurate dimensional analysis.
* **Processing options:** Allows selection between different analysis modes, such as germination, plant measurements and fpca analysis. Includes a button to store tracking visualizations for quality control.
* **Group Names:** Assigns variety identifiers to groups of seeds for experimental organization.

---

## 1. Getting Started

Begin by creating a dedicated folder for storing results, then select the first video from the Demo dataset. A popup window will prompt you to choose the appropriate folders.

![Screening Interface Getting Started](screening_images/screening_interface_germination.png)

## 2. Video Preview and Configuration

Click the **"Preview Video"** button to view your selected video. Navigate between frames using the scrollbar and press the **"S"** button to toggle the segmentation overlay for visual inspection.

![Screening Interface Video Preview](screening_images/screening_interface_video_preview_germination.png)

## 3. Calibration Setup

As this video does not have proper QR codes that are visible, we will need to manually calibrate the pixel-to-millimeter ratio.

Measure a known distance for calibration purposes. In this example, the left-to-right distance spans 11 centimeters. Use the calibration tool to determine the pixel-to-millimeter conversion ratio, particularly when QR codes are not present on the plate.

![Screening Interface Calibration](screening_images/screening_interface_calibration_germination.png)

## 4. Processing Options

Select the **"Germination"** processing option to focus the analysis on germination events. Turn off other processing options that are not relevant for this experiment.

![Screening Interface Processing Options](screening_images/screening_interface_germination_configure_processing.png)

## 5. Group Configuration

Configure the four seed groups according to your experimental design. Complete all group assignments as shown in the interface.

![Screening Interface Group Configuration](screening_images/screening_interface_germination_configure_groups.png)

## 6. ROI Selection

Use the **ROI (Region of Interest)** tool to define analysis areas for each seed group individually.

![Screening Interface ROI Selection](screening_images/screening_interface_select_roi_germination.png)

## 7. Results Monitoring

Navigate to the **Results** tab to monitor processing status and track analysis progress.

![Screening Interface Results Monitoring](screening_images/screening_interface_germination_results_tab.png)

## 8. Generating Report

Click **"Generate Report"** to generate the comprehensive final report containing all germination analysis data.

![Screening Interface Generate Report](screening_images/screening_interface_germination_report.png)

If the video was too long, and the germination time is too cramped at the beginning of the plot, you can adjust the **"End germination plot time (hours)"** parameter and reprocess the video to obtain a clearer visualization of germination events. Then, click **"Generate Report"** to update the report.

![Screening Interface Adjust End Time](screening_images/screening_interface_germination_select_end_time.png)

![Screening Interface Updated Report](screening_images/screening_interface_germination_report_2.png)