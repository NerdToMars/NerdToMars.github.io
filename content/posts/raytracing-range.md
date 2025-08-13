---
title: "Ray-Sphere Intersection: Shadow Acne"
date: 2025-07-14
draft: false
tags: ["raytracing", "mathematics", "c++", "graphics"]
---
"
There’s also a subtle bug that we need to address. A ray will attempt to accurately calculate the intersection point when it intersects with a surface. Unfortunately for us, this calculation is susceptible to floating point rounding errors which can cause the intersection point to be ever so slightly off. This means that the origin of the next ray, the ray that is randomly scattered off of the surface, is unlikely to be perfectly flush with the surface. It might be just above the surface. It might be just below the surface. If the ray's origin is just below the surface then it could intersect with that surface again. Which means that it will find the nearest surface at 𝑡=0.00000001
 or whatever floating point approximation the hit function gives us. The simplest hack to address this is just to ignore hits that are very close to the calculated intersection point"

 