![Plant Root Phenotyping Pipeline](standard_images/0.png)

To begin the plant analysis process, **launch the interface**. This will open the main analysis window. Put your mouse over any button to see a description of what it does.

![Main Interface](standard_images/1.png)

### Interface Components:

* **Select Project Folder:** Specifies the storage location for your analysis results. A project encompasses a complete experimental setup involving one or more Raspberry Pi modules.
* **Select Video Folder:** Identifies the video file for current processing. Videos must be processed sequentially, one at a time.
* **Plant Identification Fields:** The Raspberry Pi Module, Camera, Plant Number, and Identifier fields allow you to tag each plant according to its origin (camera and module), position on the plate, and biological variety.
* **Manual Calibration Parameters:** If your video does not have a 1-cm QR code, measure a known distance and write the pixels from the calibration helper.

### Getting Started:

Begin by creating a dedicated folder for storing results, then select the first video from the Demo dataset. A popup window will prompt you to choose the appropriate folders.

![Select Folders](standard_images/2.png)

---

### Video Preview and Setup:

Click the **"Preview Video"** button to view your selected video. Use the scrollbar to navigate between frames and press the **"S"** button to toggle the segmentation overlay for visual inspection. In this case, we can see that the video contains a QR code.

![Video Preview](standard_images/3.png)

Complete the plant identification details for the first plant you wish to analyze. The plant number is usually set up to identify plants from left to right in each plate.

![Plant Identification](standard_images/4.png)

---

### Plant Analysis Workflow:

1 **ROI Selection:** Click **"Analyze Plant"** to open the ROI (Region of Interest) selector. Manually define the analysis area and press double-enter to confirm your selection.

![ROI Selection](standard_images/5.png){ width="49%" } ![ROI Selected](standard_images/6.png){ width="49%" }

2 **Evaluate the segmentation quality:** Use this step to determine the correct amount of days that the segmentation can be properly analyzed. In some cases here we can determine any potential issues like plants or leaves falling down. In this case, for example we can see that after the 10th day lateral roots will be touching the next plant.

![Alt](standard_images/7.png){ width="32%" } ![Alt](standard_images/8.png){ width="32%" } ![Alt](standard_images/9.png){ width="32%" }

3 **Select the point of main root start:** This acts as a cleaning step, everything above the selected point will be discarded and not regarded as part of the root system. Please note that you can zoom in using the mouse wheel.

![Main Root Start Selection Example 1](standard_images/10.png)
![Main Root Start Selection Example 2](standard_images/11.png)
![Main Root Start Selection Example 3](standard_images/12.png)

4 **Repeat Process:** Complete this workflow for all 4 plants in the demo. Feel free to compare varieties using patterns like A-B-A-B or A-B-C-D to observe behavioral differences.

---

### Quality Control and Batch Processing:

Navigate to the **"Analysis Overview"** tab to monitor experiment progress and error rates. Poor ROI selection or incorrect seed point positioning may cause errors in graph creation. Once individual plant processing is complete, select **"Process all plants."**

![Analysis Overview Tab](standard_images/23.png)

> **PS:** In case you close the app while it was analyzing, the repeat analysis button is there for you! Just remember to delete the previous plant after relaunching it.

---

### Visual Inspection:

The **"Plant Overlay"** tab provides visual inspection capabilities for both segmentation results and plant root performance analysis. This interface allows you to discard problematic plants or restart the entire process if needed. Redoing the analysis will make you choose the ROI and root start position from scratch.

![Plant Overlay Tab](standard_images/24.png){ width="65%" }
![Plant Overlay Segmentation Toggle](standard_images/25.png){ width="28%" }

![Plant Overlay Tab 2](standard_images/26.png){ width="65%" }
![Plant Overlay Segmentation Toggle 2](standard_images/27.png){ width="28%" }

---

### Report Generation:

After completing individual plant analyses, you can generate comprehensive reports. The demo dataset includes 10 complete days of plant growth data—feel free to experiment with different report types. The system can perform interval testing (for example, every 6 hours) to compare different varieties using statistical methods such as the **Mann-Whitney U test** to determine if varieties show statistically significant differences.

> **PS:** If working with longer datasets and wanting to limit processing time, set the processing limit to your desired number of analysis days.

![Report Generation Tab](standard_images/28.png)

The system automatically generates comprehensive reports containing various figure types. All raw figures and images are saved within the report directory for detailed analysis and further investigation.

![Generated Report Example](standard_images/29.png){ width="49%" }
![Generated Report Example 2](standard_images/30.png){ width="49%" }
![Generated Report Example 3](standard_images/31.png){ width="49%" }
![Generated Report Example 4](standard_images/32.png){ width="49%" }
![Generated Report Example 5](standard_images/33.png)