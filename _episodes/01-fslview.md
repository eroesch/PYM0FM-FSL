---
title: "fslview"
teaching: 10
exercises: 5
questions:
- "Visualise and explore your data"
objectives:
- "Load fsl5.0.9 on the CINN Nutanix VM"
- "Manipulate and visualise some data"
keypoints:
- "FSL is a suite of tools"
- "fslview is such a tool, to visualise data"
- "You can launch tools from the menu, but you should know how to launch them from the command line"
---

## Load fsl5.0.9

FSL stands for fMRIB Software Library (<a href="https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/">https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/</a>). It is not a single piece of software, but a complete toolbox containing several, very specialised little tools. On the CINN Nutanix VM platform, we will use version 5.0.9, but version 6.0 exists as well. Some FSL tools are available through the menu, but we will first learn to launch them from the command line.

On the command line, type:

~~~
$ module avail
~~~
{: .language-bash}

~~~
--------------------------- /usr/share/modules/CINN ----------------------------
afni19.3.03       fieldtrip20180802 matlab/R2017b     pyBIDSconv1.1.9
anaconda2         fix1.065          pronto2.0.0       snpm13
anaconda3         freesurfer6.0.0   pronto2.0.1       spm12
conn0.18a         fsl5.0.9          pyBIDSconv1.1.5   Tarquin4.3.10
DTK_TrackVis      fsl6.0            pyBIDSconv1.1.7   Tarquin4.3.11_RC

------------------------- /usr/share/modules/versions --------------------------
3.2.10

------------------------ /usr/share/modules/modulefiles ------------------------
dot           module-git    modules       use.own
matlab/R2017b module-info   null
~~~
{: .output}

“module” is a little tool that provides the ability to configure the system. In CINN, we use it to make sure that we can access several versions of the same software, without them colliding with each other. The command “module avail” shows all the modules that are available. Type:

~~~
$ module load fsl5.0.9
~~~
{: .language-bash}

This will load the module for fsl version 5.0.9. There is also a second version available, v6, but for PYM0FM, we will stick to using v5.

Start FSLView by typing

~~~
$ fslview &
~~~
{: .language-bash}

The "&" means that the program you asked for (fslview) runs in the background in the terminal (or shell), and you can keep typing other commands while it is running. If you had not done that then you would not be able to do anything else in the terminal until you killed fslview (or, alternatively, you could type control-z in the terminal and then "bg" to get fslview running in the background post-hoc).

Load in the image example_func.nii.gz, by pressing File -> Open and selecting the image.

Hold the mouse button down in one of the view panels and move it around - see how various things update as you do so:
* the other panels update their view 
* the cursor's position in both voxel and mm co-ordinates gets updated (hover your mouse over the X Y and Z coordinate boxes to find out from “tooltips” which boxes give the values in voxels, and which boxes give the values in mm)
* the image intensity at the cursor is shown 

<a href="{{ page.root }}/fig/fslview-modetoolbar.png">
  <img src="{{ page.root }}/fig/fslview-modetoolbar.png" width="250px"/>
</a>

Now click several times on the small upwards arrow [1] (on some computers the arrows are replaced with a small "+" and "-") by the scale control (currently showing "100%"). This is one way of controlling the zoom. If you click on the icon of a hand [3] you can drag a view around. You can reset the view settings by pressing on the button with the arrow on top of the magnifying glass [6]. You can also set the field-of-view of a panel by clicking on the button with the magnifying glass [5], and then click-and-dragging the mouse in a view panel. Return to "normal view mode" (as opposed to "move" or "zoom" mode) by clicking on the button with the small cross [2].

<a href="{{ page.root }}/fig/fslview-bricon.png">
  <img src="{{ page.root }}/fig/fslview-bricon.png" width="250px"/>
</a>

You can control the brightness and contrast either by using the wheels/sliders [3] near the "brightness/contrast" button [2] (this button allows you to reset the brightness and contrast to their initial settings). You can also control the intensity display range explicitly by typing numbers into the Min and Max boxes [1].

Open a lightbox view using Tools -> Lightbox. This will produce a set of axial (transverse) slices. If you drag the mouse around in the viewer you can see that the cursor position is linked in the two views of the data. This is particularly useful when you have several images loaded in at the same time.

If you increase the % zoom in the lightbox mode sufficiently, you will get a scrollbar to let you control which slices you are viewing. Kill the lightbox view now and expand the ortho view back to full size. 

<a href="{{ page.root }}/fig/fslview-layers.png">
  <img src="{{ page.root }}/fig/fslview-layers.png" width="250px"/>
</a>

Now load in a second image using File -> Add; thresh_zstat1 is a thresholded FMRI stats image. In the bottom-right panel is a list of loaded images - the layer toolbar. Images can be turned on and off by double-clicking in that list [7] (or by highlighting the image in the list [8] and then clicking on the checkbox by the small eye icon [1] at the bottom). Once highlighted in the image list, an image's transparency can be changed with the slider [3] (at the bottom of the box); reduce the "solidity" of the stats overlay image.

Also, when an image in the image list is highlighted:
* You can click on the i button [6] and change the image's colour display scheme (LUT - look-up-table), and see/change some other basic image information. 
* You can set the brightness/contrast settings for that image, as described above. 
* You can view voxel intensities for that image in the normal place (to the right of the voxel co-ordinate displays). 

<a href="{{ page.root }}/fig/fslview-view.png">
  <img src="{{ page.root }}/fig/fslview-view.png" width="80px"/>
</a>

Now close down all views; all loaded images have now been deleted from FSLView. Next, load in filtered_func_data, a 4D FMRI time series. Now watch this as a movie by pressing the film-strip button [1] that appears when a 4D file is loaded as the primary image (the first image to be loaded). You will see the time-counter ("Volume") scrolling through the different time-point values. Note that whilst the movie is running you can still change the cursor position. You can even re-load the thresh_zstat1 stats overlay image back in whilst the movie is running. Stop the movie by pressing the movie button again.

Looking at a movie of your 4D time series data is a very good way of spotting problems with the data such as excessive head motion, sudden image intensity changes (spikes), and ghosting. It is always worth doing this as an initial quality check on your data.
To illustrate this, load in an a 4D FMRI time series acquired while one of my collaborators dozed off in the scanner instead of attending to the experiment. Close down the current view and load the file headMotion and watch it as a movie.

These images have not had any motion correction or smoothing applied, they are “fresh from the scanner”, unlike the last movie you viewed where the images had already been preprocessed.

<a href="{{ page.root }}/fig/fslview-timeseries.png">
  <img src="{{ page.root }}/fig/fslview-timeseries.png" width="250px"/>
</a>

Close the headMotion data series and open filtered_func_data again. Open a timeseries graph view with Tools -> Timeseries (you will need to have the 4D dataset highlighted in the image list for this option to be active). Move around with the mouse button held down until you are on a "highly activated" voxel. Press the + button [1] in the timeseries view and that voxel's timeseries gets saved in the display. You can add more timeseries by moving to new voxels and pressing + again.

If you have used "+" to add several timeseries to the display they may all have quite different mean values, making comparison difficult - press the "-μ" button [3] to demean all viewed timeseries. Once you have turned on demeaning you can also choose to turn on the "%" button [4], which shows the y-axis as a % of the mean level (i.e. in this case you're now seeing the BOLD % signal change values). 

<a href="{{ page.root }}/fig/fslview-histogram.png">
  <img src="{{ page.root }}/fig/fslview-histogram.png" width="120px"/>
</a>

To view a basic histogram of the currently displayed image press Tools -> Image histogram. A histogram plots the distribution of intensities in the image; image intensity is on the x axis and the number of voxels with that intensity is on the y axis. View the histogram of example_func; you can click in the histogram to view exact values, which appear at the bottom left. Click on the toolbox button [3] to get more histogram options. If you have time take a look at some voxel time series plots and an image histogram for the headMotion file.

Finally, we'll look at some more advanced FMRI analysis features in FSLView. Kill FSLView and enter the following (remember to use the tab key to speed up typing)

~~~
$ cd /storage/silver/pym0fm/<YOUR ITS LOGIN>/fsl_course_data/fmri/ptt/at/at_left.feat
~~~
{: .language-bash}

You are now in an example FMRI analysis FEAT output directory. Note, FEAT is the program that you will use next week to find activations in 4D functional data. Type
~~~
$ fslview filtered_func_data thresh_zstat1 thresh_zstat2 &
~~~
{: .language-bash}

The image names on the fslview command line tell FSLView to load in each of these images, to save you having to load them in by hand in the GUI. Because FSLView detects that you are in a FEAT directory it automatically turns on timeseries viewing. You might want to resize the FSLView window (make it wider) and then auto-resize the inner windows with Window -> Tile.

One of the nice features when in "FEAT mode" is that you can see a plot of the fitted timeseries model versus the data - in the timeseries window change No model to Full model only (timeseries toolbar [6]). Now when you click around in the image you can see not just the data timeseries but also the fitted model.

The other nice feature is the cluster browser - turn this on with Tools -> Cluster browser. This lets you select a stats image name and get summary information about the different activation clusters found by FEAT. You can even click on a row in the cluster table and FSLView will take you to the peak voxel in that cluster

This FEAT output directory already contains versions of some of the images upsampled to "standard space" - the common image space that multisubject analyses are carried out in. Kill fslview and run: (note: only press return once you have typed in both lines of this)
$ fslview reg_standard/reg/highres.nii.gz reg_standard/stats/cope1 -l Red-Yellow -b 100,400

The options tell FSLView what colourmap to use for the FMRI activation effect size image cope1, and what intensity display range. Note that the Min intensity display range value has the effect of thresholding the image it is applied to.
Because these images are in standard space we can turn on the atlas tools with Tools -> Toolbars -> Atlas Tools. Now as you click around in the image you can see reporting of the probability of being in different brain structures. The atlases that are turned on by default are the Harvard-Oxford cortical and subcortical atlases, but you can also choose others by pressing the Atlases... button. These are formed by averaging careful hand segmentations of structural images of many separate individuals. Find the thalamus (left or right); you can see that there is activation here.

You can turn on summary images of atlases by double-clicking on the name inside the Atlases... popup window; have a play with that. Finally, bring up the Structures... window, turn on the two tickboxes, and then click around in the list of structures. For those atlases which are probabilistic, this shows a single structure at a time, with the full probability information shown as a gradation of colour. The Structures... window is useful when you know the name of a brain area from a paper or talk, but you don’t know where it is anatomically.

Note that FSLview can also render 3D images of brains with activation shown. How to do this is documented in the online tutorial on the FSL website.

{% include links.md %}
