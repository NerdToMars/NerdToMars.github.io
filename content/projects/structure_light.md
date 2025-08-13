+++
title = "A High-accuracy Structure Light Scanner"
description = "A high-accuracy structure light scanner based on a custom-built projector and a high-resolution camera"
weight = 1

[extra]
# local_image = "project-1.jpg"
# link_to = "https://github.com/NerdToMars/nerf-rust/tree/main/src"
+++

<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; margin: 2rem 0;">
    <iframe 
        src="https://www.youtube.com/embed/ecDD_nABdoE" 
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;" 
        allowfullscreen 
        title="Structure Light Scanner Video">
    </iframe>
</div>

This project is a high-accuracy structure light scanner based on a custom-built projector and a high-resolution camera. It is used to scan the surface of an object and generate a point cloud of the object.

The 3D visualization is built on top of potree.js. The point cloud is generated using the structure light scanner and the 3D reconstruction computation is done on the CUDA GPU.
