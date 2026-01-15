# Root Analysis – Tomato (Standard Interface)
    
![Plant Root Phenotyping Pipeline](standard_tomato_images/0.png)

To begin the plant analysis process, **launch the interface**. This will open the main analysis window. Put your mouse over any button to see a description of what it does.

### Interface Components:

* **Select Project Folder:** Specifies the storage location for your analysis results. A project encompasses a complete experimental setup involving one or more Raspberry Pi modules.
* **Select Video Folder:** Identifies the video file for current processing. Videos must be processed sequentially, one at a time.
* **Plant Identification Fields:** The Raspberry Pi Module, Camera, Plant Number, and Identifier fields allow you to tag each plant according to its origin (camera and module), position on the plate, and biological variety.
* **Manual Calibration Parameters:** If your video does not have a 1-cm QR code, measure a known distance and write the pixels from the calibration helper.

### Getting Started:

Begin by creating a dedicated folder for storing results, then select the first video from the Demo dataset. A popup window will prompt you to choose the appropriate folders.

![Select Folders](standard_tomato_images/1.png)

---

### Video Preview and Setup:

Click the **"Preview Video"** button to view your selected video. Use the scrollbar to navigate between frames and press the **"S"** button to toggle the segmentation overlay for visual inspection. In this case, we can see that the video contains a QR code.

![Video Preview](standard_tomato_images/2.png){ width="49%" }
![Plant Identification](standard_tomato_images/3.png){ width="49%" }

### Using the calibration helper to complete the distances:

As these demo plates do not contain QR codes we can use the known distance on the center of the plate, the
visible area given by the plate holder is 11 centimers, and according to the calibrator, those measure ~2600
pixels.

![Calibration Helper](standard_tomato_images/4.png)
![Calibration Helper Measurement](standard_tomato_images/5.png)

---

### Plant Analysis Workflow:

1 **ROI Selection:** Click **"Analyze Plant"** to open the ROI (Region of Interest) selector. Manually define the analysis area and press double-enter to confirm your selection.

![ROI Selection](standard_tomato_images/6.png){ width="49%" } ![ROI Selected](standard_tomato_images/7.png){ width="49%" }

2 **Evaluate the segmentation quality:** Use this step to determine the correct amount of days that the
segmentation can be properly analyzed. In some cases here we can determine any potential issues. In this
case we can see that we need to be careful with the main root positioning as we may era some potential
lateral roots.

![Alt](standard_tomato_images/8.png){ width="23%" } ![Alt](standard_tomato_images/9.png){ width="23%" } ![Alt](standard_tomato_images/10.png){ width="23%" } ![Alt](standard_tomato_images/11.png){ width="23%" }

3 **Select the point of main root start:** This acts as a cleaning step, everything above the selected point will
be discarded and not regarded as part of the root system. Please note that you can zoom in using the mouse
wheel.

We select the two plants of the first camera with identifier A.

![Main Root Start Selection Example 3](standard_tomato_images/12.png){ width="49%" }
![Main Root Start Selection Example 4](standard_tomato_images/13.png){ width="49%" 

For the second camera, root start selection can be trickier.

![Main Root Start Selection Example 5](standard_tomato_images/14.png){ width="49%" }
![Main Root Start Selection Example 6](standard_tomato_images/15.png){ width="49%" }

But in this kind of cases, do not worry! Selecting above the root will also help, as we can see there are not any miss-detections that can cause us any trouble. 

![Main Root Start Selection Example 7](standard_tomato_images/16.png){ width="31%" }
![Main Root Start Selection Example 8](standard_tomato_images/17.png){ width="31%" }
![Main Root Start Selection Example 9](standard_tomato_images/18.png){ width="31%" }

Then the last plant:

![Main Root Start Selection Example 10](standard_tomato_images/19.png){ width="49%" }
![Main Root Start Selection Example 11](standard_tomato_images/20.png){ width="49%" }

---

### Quality Control and Batch Processing:

Navigate to the **"Analysis Overview"** tab to monitor experiment progress and error rates. Poor ROI selection or incorrect seed point positioning may cause errors in graph creation. Once individual plant processing is complete, select **"Process all plants."**

![Analysis Overview Tab](standard_tomato_images/21.png)

> **PS:** In case you close the app while it was analyzing, the repeat analysis button is there for you! Just remember to delete the previous plant after relaunching it.

---

### Visual Inspection:

The **"Plant Overlay"** tab provides visual inspection capabilities for both segmentation results and plant root performance analysis. This interface allows you to discard problematic plants or restart the entire process if needed. Redoing the analysis will make you choose the ROI and root start position from scratch.

![Plant Overlay Tab](standard_tomato_images/22.png){ width="65%" }
![Plant Overlay Segmentation Toggle](standard_tomato_images/23.png){ width="28%" }

Above we can see a stop of growth in the main root due to the plant reaching the bottom of the plate. This should normally mark the end of the experiment. Meanwhile, plants of plate A still have not reached the base; we can see this as the main root length does not stagnate. But we need to be careful, because that can also happen if the bounding box is not properly chosen (does not give space to grow).

![Plant Overlay Tab 2](standard_tomato_images/24.png){ width="48%" }
![Plant Overlay Segmentation Toggle 2](standard_tomato_images/25.png){ width="48%" }

---

### Report Generation:

After completing individual plant analyses, you can generate comprehensive reports. The demo dataset includes 10 complete days of plant growth data—feel free to experiment with different report types. The system can perform interval testing (for example, every 6 hours) to compare different varieties using statistical methods such as the **Mann-Whitney U test** to determine if varieties show statistically significant differences.

> **PS:** If working with longer datasets and wanting to limit processing time, set the processing limit to your desired number of analysis days.

![Report Generation Tab](standard_tomato_images/26.png)

The system automatically generates comprehensive reports containing various figure types. All raw figures and images are saved within the report directory for detailed analysis and further investigation.

![Generated Report Example](standard_tomato_images/27.png){ width="49%" }
![Generated Report Example 2](standard_tomato_images/28.png){ width="49%" }
![Generated Report Example 3](standard_tomato_images/29.png){ width="49%" }