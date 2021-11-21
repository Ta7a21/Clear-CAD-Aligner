# Using OBBTree for Jaws Alignment
## About OBBTree
An oriented bounding box (OBB) is a bounding box that does not necessarily line up along coordinate axes. The OBB tree is a hierarchical tree structure of such boxes, where deeper levels of OBB confine smaller regions of space. A good reference for OBB-trees is [Gottschalk & Manocha in Proceedings of Siggraph `96](https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.580.5054&rep=rep1&type=pdf). For visualization please refer to this [video](https://www.youtube.com/watch?v=dHt6v1MjMhE)

## Using OBBTree in alignment
After creating the oriented bounding boxes for the source and target, we use a VTK library called [vtkLandmarkTransform](https://vtk.org/doc/nightly/html/classvtkLandmarkTransform.html#a8edf745c82c2c3f55fe227172cea8fd0) to orient the source bounding box with four rotations in the XYZ axis to get the best fit for the target bounding box, and then compute the relative and Hausdorff distances from the two sets of points of the boxes using [vtkHausdorffDistancePointSetFilter](https://vtk.org/doc/nightly/html/classvtkHausdorffDistancePointSetFilter.html#details) to see which rotation fits the best. The source best points are then aligned with the target best points using a different transformation matrix.

## Results
We tested the algorithm on a set of 42 jaws on different target jaws. With Niemann Carrie's jaw as a target, 35 of them aligned correctly while 7 of them didn't align (4 of them were incomplete jaws, and the other 3 had an original orientation that fits best when rotated with the incorrect direction). When we used another jaws as a target we had random results (Some of the correctly aligned jaws didn't line up with different target jaws, while others did).

## Screenshots
### Successful Alignments
![image](https://cdn.discordapp.com/attachments/881646256085155922/912008807658426378/unknown.png)
![image](https://cdn.discordapp.com/attachments/881646256085155922/912027424949145650/unknown.png)
![image](https://cdn.discordapp.com/attachments/881646256085155922/912030015716208710/unknown.png)
![image](https://cdn.discordapp.com/attachments/881646256085155922/912030460383735908/unknown.png)
![image](https://cdn.discordapp.com/attachments/881646256085155922/912031004120727572/unknown.png)
### Unsuccessful Alignments
![image](https://cdn.discordapp.com/attachments/881646256085155922/912011157638881340/unknown.png)
![image](https://cdn.discordapp.com/attachments/881646256085155922/912011636892655696/unknown.png)
### Incomplete Jaws
![image](https://cdn.discordapp.com/attachments/881646256085155922/911989072183058483/unknown.png)
### Possible-to-fail Orientation
![image](https://cdn.discordapp.com/attachments/881646256085155922/911732444233879562/unknown.png
)
