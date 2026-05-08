Advanced Computer Vision

How to stabilize image mosaics:
1) **Registration to stabilize the mosaics**
2) **alignment to perform stitches problem**
3) **Robust estimation (e.g. RANSAC)**

The main problem is the matching of the points that we want to stitch, there are several methods including RANSAC.

Solution 2.2

>[!note] Global Consistency and Drift Control (Global Optimization / Loop Constraints)
>In the mosaics there will always be small errors over time, they can cause drift and deform the mosaic. We can mitigate these errors. It s not possible in a real case to do it pixel by pixel.
>>[!tip] Global Consistency 
>>Instead of trusting only local pairwise matches, it adjusts transformations across many frames together, so the full mosaic remains coherent overall.
>
>>[!tip] Loop Constraints
>>



