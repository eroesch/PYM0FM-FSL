---
title: "fslview"
teaching: 0
exercises: 0
questions:
- "Visualise and explore your data"
objectives:
- "First learning objective. (FIXME)"
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
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
  <img src="{{ page.root }}/fig/fslview-modetoolbar.png"/>
</a>

Now click several times on the small upwards arrow [1] (on some computers the arrows are replaced with a small "+" and "-") by the scale control (currently showing "100%"). This is one way of controlling the zoom. If you click on the icon of a hand [3] you can drag a view around. You can reset the view settings by pressing on the button with the arrow on top of the magnifying glass [6]. You can also set the field-of-view of a panel by clicking on the button with the magnifying glass [5], and then click-and-dragging the mouse in a view panel. Return to "normal view mode" (as opposed to "move" or "zoom" mode) by clicking on the button with the small cross [2].


{% include links.md %}

