---
title: "Brain Extraction Tool (BET)"
teaching: 0
exercises: 0
questions:
- ""
objectives:
- "First learning objective. (FIXME)"
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---

## Introduction

<a href="https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/BET">BET</a> is a tool that will carve out non-brain tissue from an volume of the whole head.

Most FSL programs can be run from the command-line without using a GUI, by typing fully lowercase names (e.g. bet). Most programs also have a GUI, which can be started via the fsl mini-GUI (type fsl &) or by typing a capitalised version of the command name (e.g. Bet &).
In any analysis, you should use the GUI to explore the data and try out analyses, but really, if you are going to do any serious analyses, you should write a script that will call out the tools you use.

For those FSL programs that can be run from the command line without a GUI the usage can be obtained by typing the lowercase name. Type bet and press return to see the usage for bet. This tells you that to use bet from the command line you need to give it the name of an input images, a filename for the output images, and you can also choose various options concerning the output and how brain extraction is achieved. Start the fsl GUI and click on BET, to see how this all works. Now exit both of these GUIs and start the Bet GUI directly from the terminal.

Using the Bet GUI, set the input file to structural; use the right-hand file selector rather than typing this in by hand. Turn on various optional outputs (brain extracted image, binary brain mask and skull surface image - see Advanced Options tab) but leave the other settings as they are. Note that the GUI suggests the default output name structural_brain. When done click on "Go" to run BET and then exit the GUI once it's done.

Use ls to see what files got created and view the various outputs. Hint: if you type

~~~
$ ls -lrt
~~~
{: .language-bash}

then the listing is sorted according to file creation date, hence it's very easy to see what the most recently created files in a directory are. View the brain mask overlaid onto the original image by first loading the original image into fslview and then adding the mask image. Change the transparency of the overlay so that you can get a better view of the success of the brain extraction. 

Type bet to get the usage description again and make sure you understand the command that the GUI printed in the terminal when you pressed OK. Advanced use of BET to deal with problematic images is dealt with at the end of this document.

### Intra-subject registration

An imaging session with a single subject usually results in several different kinds of images that have different dimensions (e.g. the structural has much smaller voxels than functional images, and therefore far more voxels). Intra-subject registration is the process of establishing a mapping between the two images, effectively “lining them up with each other”.

~~~
$ cd /storage/silver/pym0fm/<YOUR ITS LOGIN>/fsl_course_data/reg 
~~~
{: .language-bash}

We start by using FLIRT for image-to-image registration within a single subject. The images we start with in this example are of a different modality (T1-weighted and T2-weighted), and are called sub2_t1 and sub2_t2.
* Apply BET before FLIRT
Apply BET to the images sub2_t1 and sub2_t2 (saving the results as sub2_t1_brain and sub2_t2_brain). Check the outputs in FSLView - note that these do not need to be "perfect" but should have removed the majority of the non-brain structures without removing any of the brain material. It doesn't matter if there are some differences between them, especially around the eyeballs.
* Registration using the FLIRT GUI
Start the FLIRT GUI (using "Flirt &" or "Flirt_gui &") and register sub2_t2_brain (input image) to sub2_t1_brain (reference image). Note that to make the file browser for the reference image go to the local directory (and not the directory containing the template images) just erase the contents of the "Filter" box (at the top) and press return.
Choose 6 DOF (which is not the default) since these images are from the same subject. 6 DOF implements a rigid body transform, made up of 3 directions of translation and 3 directions of rotation. Because the images are from the same subject you don’t want any expansion, contraction or shearing as part of the matching process. Choose Correlation Ratio as the cost function (which is the default) as the images are different modalities. (Mutual information is the most accurate, but it takes longer)
Save the output image as a name of your choice. This will take a few minutes to run...

•	While you wait... 
Load the input and reference volumes into FSLView (note that this is normally not possible as FSLView requires the two images to have the same resolution and FOV, which this pair just happens to have but it is not the norm). Once these are loaded, try to see the difference by flicking between them: that is, by turning the "top" one off and on (i.e. making them visible or not in the image list - by changing the "eye" symbol). Another way of comparing, which reduces the load on your visual short term memory, is to use the transparency slider to gradually make one of the images transparent, revealing the image underneath.
•	Visual Check - FSLView 
Once FLIRT has finished, add the resulting transformed image (output) to FSLView. Compare it to the reference image and the input image. Try to see the differences by flicking between pairs of images. Make sure that you only have two of them visible at any one time. 
Flicking between images is a very good way of detecting registration differences and changes. Normally this can only be done for the reference and output images from FLIRT, as it is unusual that pre- and post- registered images share a common resolution and FOV like these do. 
•	Visual Check - slices 
Now use slices to look at the result (the file output_image or whatever you have called it instead) by running: 
$ slices output_image sub2_t1_brain 
The red lines are edges generated from the second image (sub2_t1_brain) and should be aligned with edges in the output image, although sometimes they will show small differences in the BET masking around the outer brain surface. For comparison, also run slices on the reference image and the original image sub2_t1_brain and sub2_t2_brain. The misalignment is much greater at the back of the brain in this image pair.





{% include links.md %}
