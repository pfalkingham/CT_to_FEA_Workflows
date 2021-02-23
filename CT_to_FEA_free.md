# A free workflow from CT scan to FEA

Originally from [this blog post](https://peterfalkingham.com/2020/11/06/a-free-opensource-workflow-from-ct-scan-to-fea/)

I’ve spent quite a bit of time this year trying to find a good workflow for carrying out finite element analysis (FEA) using only free software. I think I’ve finally got a workflow that works.

Disclaimer: FEA is way more complex than just making colourful stress maps. Whilst the info on this page gives you a workflow, you still need to put in the research hours to figure out what kind of mesh you want, what material properties, and what loads you should use!

## CT Data to model

I’ve previously given a full workflow for [3D Slicer](https://peterfalkingham.com/2015/03/12/227/), from [CT scan to 3D print](https://peterfalkingham.com/2018/04/29/ct-data-to-3d-print-in-15-minutes-using-free-software/). The same principle applies. Here, I’ve used ORS Dragonfly, which isn’t open source but is free for non-commercial research. I really like Dragonfly, mainly because of it’s nice renderer, but also because it’s just easier to use the Slicer, in my opinion. You can use anything though, and [I‘ve previously written a list of free CT segmentation software packages](https://peterfalkingham.com/2019/02/18/free-software-for-ct-segmentation-2019/) that you might find useful.

<iframe width="560" height="315" src="https://www.youtube.com/embed/Xtu6437j1bA" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

After getting out a model, we need to make sure it’s manifold (watertight), and oriented in such a way that applying loads and constraints is simple (i.e. aligning the directions of forces with world axes). To do this, I used Blender. I used the voxel remesher and 3d print add on to make sure the mesh was watertight but still retained the detail:

<iframe width="560" height="315" src="https://www.youtube.com/embed/3iC0nBsbz54" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

What I don’t show in the above video is that I then used the quadriflow remesher to get face count down to 10,000, just so the model was small enough to import and run in the FEA software in a reasonable amount of time.

To carry out the FEA I used [FEBio Studio](https://febio.org/). This is an all-in-one freely available software that can mesh and run the analysis. Again, I wizzed through with not particularly well thought out meshing and materials/loads – if you want to do serious FEA you’ll need to spend plenty of time figuring out what are the best parameters.

<iframe width="560" height="315" src="https://www.youtube.com/embed/SaNPOW26nuY" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

And there we are. Total time taken over the three videos is about 12 minutes, from raw CT scan data to FEA results.
