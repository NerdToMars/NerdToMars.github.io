---
title: "Ray-Sphere Intersection: A Subtle Bug with Dot Products"
date: 2025-07-14
draft: false
tags: ["raytracing", "mathematics", "c++", "graphics"]
---

## The Ray-Sphere Intersection Problem

When implementing ray tracing, one of the fundamental operations is determining whether a ray intersects with a sphere. This involves solving a quadratic equation derived from the sphere's mathematical definition.

### The Mathematical Foundation

A sphere with radius $r$ centered at point $\mathbf{C}$ is defined by the equation:

$$(\mathbf{C} - \mathbf{P}) \cdot (\mathbf{C} - \mathbf{P}) = r^2$$

Where $\mathbf{P}$ is any point on the sphere's surface. For a ray defined as $\mathbf{P}(t) = \mathbf{Q} + t\mathbf{d}$, we substitute to find intersection points:

$$(\mathbf{C} - (\mathbf{Q} + t\mathbf{d})) \cdot (\mathbf{C} - (\mathbf{Q} + t\mathbf{d})) = r^2$$

Expanding this using vector algebra:

$$t^2\mathbf{d} \cdot \mathbf{d} - 2t\mathbf{d} \cdot (\mathbf{C} - \mathbf{Q}) + (\mathbf{C} - \mathbf{Q}) \cdot (\mathbf{C} - \mathbf{Q}) - r^2 = 0$$

## The Subtle Bug

The tricky part isn't just knowing that dot products and multiplications are different - it's knowing **when to use which one** when translating mathematical formulas to code.

Let's look at the discriminant formula:

$$\Delta = b^2 - 4ac$$

Where:
- $a = \mathbf{d} \cdot \mathbf{d}$ (scalar)
- $b = -2\mathbf{d} \cdot \mathbf{oc}$ (scalar) 
- $c = \mathbf{oc} \cdot \mathbf{oc} - r^2$ (scalar)

**The key insight**: Once you've computed the dot products, you're working with **scalars**, so you use regular multiplication.

Here's the incorrect implementation that confuses this:

```cpp
// INCORRECT - mixing up when to use * vs dot()
vec3 oc = center - r.origin();
auto direction_square = dot(r.direction(), r.direction());  // scalar
double oc_oc = dot(oc, oc);  // scalar

auto d = oc_oc * direction_square - direction_square * (oc_oc - radius * radius);
return d > 0;
```

**What went wrong?** The code correctly computed the dot products to get scalars, but then tried to "reconstruct" the discriminant formula incorrectly. It should have used the standard quadratic formula: $b^2 - 4ac$.

## The Correct Implementation

```cpp
vec3 oc = center - r.origin();
auto a = dot(r.direction(), r.direction());
auto b = -2.0 * dot(r.direction(), oc);  // Note the -2.0 factor
auto c = dot(oc, oc) - radius * radius;
auto discriminant = b * b - 4.0 * a * c;  // Standard quadratic formula
return (discriminant >= 0);
```

## The Rule: Follow the Mathematical Formula Exactly

The golden rule: **Once you've computed all dot products, you're working with scalars and should follow the mathematical formula exactly.**

Here's the step-by-step process:

1. **Identify dot products in the formula**: Look for $\mathbf{a} \cdot \mathbf{b}$ patterns
2. **Compute them first**: `auto a = dot(d, d); auto b = dot(d, oc);`
3. **Apply the mathematical formula**: Use regular multiplication for the final calculation

```cpp
// Step 1: Compute dot products to get scalars
auto a = dot(r.direction(), r.direction());  // scalar
auto b = -2.0 * dot(r.direction(), oc);      // scalar  
auto c = dot(oc, oc) - radius * radius;      // scalar

// Step 2: Apply the quadratic formula exactly
auto discriminant = b * b - 4.0 * a * c;     // all scalars, use *
```

## Key Takeaways

1. **Dot products → scalars**: `dot(vec3, vec3)` always returns a scalar
2. **Scalars → multiplication**: Once you have scalars, use `*` not `dot()`
3. **Follow the formula**: Don't try to "reconstruct" the math - use the standard quadratic formula
4. **Check your types**: If you're multiplying two `double` values, you want `*`, not `dot()`

The bug happens when you forget that dot products reduce vectors to scalars, and then try to "reconstruct" the original vector math instead of following the simplified scalar formula.

# Reference

Reference: [Ray Tracing in One Weekend - Adding a Sphere](https://raytracing.github.io/books/RayTracingInOneWeekend.html#addingasphere)