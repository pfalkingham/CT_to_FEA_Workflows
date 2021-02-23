# A rough guide to getting models out of CT scans using 3D Slicer (v4)

(Originally from [This blog post](https://peterfalkingham.com/2015/03/12/227/), and before that, [a PDF I put on Academia.edu](https://www.academia.edu/11395348/A_rough_guide_to_getting_models_out_of_CT_scans_using_3D_Slicer_v4_))


This guide will hopefully provide a quick start to processing CT data and exporting models using 3D slicer (http://download.slicer.org/). The documentation available for Slicer is pretty fragmented and/or out of date (referring to considerably older versions), so this guide is based on quite a bit of trial and error. However, hopefully it can provide PC users with an easy enough alternative to Osirix.

## Importing Data

I’ll assume that you have your raw data in the form of DICOMS, though 3D Slicer opens many formats. By default, Slicer opens to the welcome pane:

![](https://pfalkingham.files.wordpress.com/2015/03/slicer1.png?w=474)

Clicking on ‘Load DICOM data’ in the upper left will do just that:

![](https://pfalkingham.files.wordpress.com/2015/03/slicer2.png?w=474)

Hit import and find the directory that the DICOM files are in. Make sure everything seems as it should. When you click on the new entry, a scalar volume will appear in the lower box. Make sure this is checked, and then click ‘Load Selection to Slicer’.

## Visualizing the data

Now the data is loaded into Slicer, you should see it in the red/yellow/green windows (slices from various views), but the 3D view will be empty. In order to see something, we’re going to need to threshold the data, and set it to visible. Use the drop down menu for selecting modules and choose ‘Volume Rendering’ (1, image below). Click the closed eye icon (2, image below) to make the volume visible in the 3D view. This should make the whole volume appear, but in order to see bones/features of interest, we’ll have to threshold this. This is done by first expanding the ‘Advanced’ section (3) and then moving the middle circle (4) to alter transparency (vertical) and threshold (horizontal). Note that this is not making models, this is just visualising the data.

![](https://pfalkingham.files.wordpress.com/2015/03/slicer3.png?w=474)

You'll need to centre the view on the data, if your CT isn’t placed at the origin. There's a button above each view that does that.

## Segmenting the data

In order to segment the data, we need to go to the Editor module (same place you previously selected ‘Volume Rendering’ above). Click apply when it asks you the colours to use (unless you want to play around with colour sets, but for the purposes of this guide that is unnecessary).

In the editor view, we have tools to threshold, paint, etc. Again, for simplicity’s sake I’ll assume that here we’re just trying to get models of a skeleton. The best place to start is with the threshold button:

![](https://pfalkingham.files.wordpress.com/2015/03/slicer5.png?w=474)

Move the slider until the objects you want are coloured (by default, label 1 is green, so your slice views will be flashing green), and background is not, then hit apply.

If you want to see how well this is working, head back to the ‘Volume Rendering’ module and change the Volume from ‘Unknown’ to ‘Unknown-label’:

![](https://pfalkingham.files.wordpress.com/2015/03/slicer6.png?w=474)

This will visualise what you’ve just thresholded.

Of course, now we return to the Editor, if you want to lower the threshold for that label, you’ll need to first delete the label with this: ![](https://pfalkingham.files.wordpress.com/2015/03/slicer7.png). In addition to thresholding, you can use the Paint tool ![](https://pfalkingham.files.wordpress.com/2015/03/slicer8.png) to paint directly on slices, or a tool I find very useful is the island tools – keep island (![](https://pfalkingham.files.wordpress.com/2015/03/slicer9.png)) and remove island (![](https://pfalkingham.files.wordpress.com/2015/03/slicer10.png)) where you click on the island (in the slice views) you want to keep/remove, for instance if you have isolated bones from a disarticulated specimen.

You can either click on the coloured rectangle or use the up/down buttons to change label and identify different things.

Painting and thresholding might take some work depending on your data.

## Exporting models

When you are happy with your labelling and segmenting, it’s time to make the models for export. In the Editor module, click the Make Model button (![](https://pfalkingham.files.wordpress.com/2015/03/slicer11.png)), and then hit ‘go to model maker.’

Where it says ‘Select a ModelHierarchy’, choose ‘Create new ModelHeirarchy.’

You can play with the settings in here, to alter smoothing etc, and then hit apply. You’re 3D models will now appear in the 3D view. To export them, go to file->save and select the vtk files. You can change vtk format to stl or ply at this point. With the models selected, choose an output directory and save.

You should now have several VTK/STL/PLY files in the directory of your choice.