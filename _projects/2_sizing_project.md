---
layout: page
title: Aircraft Initial Sizing Tool
# description: a project with a background image and giscus comments
img: assets/img/sizing_cover.png
importance: 1
category: work
---

Given requirements for an aircraft design such as a required range, service ceiling and balanced field length (BFL), how do we find a 'starting point': wing shape, wing size and engine size? This starting point lets us kick off the design loop where we then create more detailed designs using higher fidelity analyses. The answer is, we need a *sizing* tool. 

This project was kicked off as a project for AE 442, the Senior Design course at the University of Illinois. So, how do we size an aircraft? We must start with a 'seed' aircraft, with a similar purpose/mission to the aircraft we are designing. For instance, if we were trying to design a 160 seat narrow-body aircraft, we would probably choose an A220-300, B737 MAX 7 or A319neo. We use this aircraft to tune our baseline aerodynamic estimations, engine / takeoff performance characteristics, etc. until they are fairly accurate. 

After we have tuned our estimations, we use our mission requirements to adjust the aircraft in the design direction which pushes us closer to meeting our requirements. For instance, if we do not meet the required range, we would increase the size of the fuel tank. Similarly, if we do not meet our service ceiling or BFL requirements, we would increase the size (and therefore thrust output) of our engine. With this sizing algorith, we choose which parameters we adjust to meet each requirement. 

The choice of parameters we made for this project allow us to conduct parametric sweeps, evaluating the impact of, say, wing size and aspect ratio on a sized aircraft's empty weight or mission fuel burn. Often, the most efficient aircraft (i.e., the one with the lowest fuel burn) is not the aircraft we design, because these designs often require a high aspect ratio (AR) which results in a heavier (and therefore, more expensive) wing.

To enable faster parametric sweeps, I introduced multi-threading capability, resulting in a ~10x speedup in parametric sweep time on my 12-core Laptop CPU, though larger improvements are likely for beefier Desktop CPUs. Additionally, this code would be very easy to rewrite in a language like FORTRAN or C, which would undoubtedly result in a massive throughput increase. However, Python has access to much more user-friendly graphing libraries like matplotlib.

Here are some of the results when sizing an F/A-18 style aircraft for a simplified set of requirements from the AIAA 2025-26 student design competition. Here is an example sizing contour plot for an F/A-18 redesigned with 600nm of additional range:

<div class="col-sm-12 mx-auto">
    {% include figure.liquid loading="eager" path="assets/img/sizing1.png" title="example image" class="img-fluid rounded z-depth-1" %}
</div>

Do note how different the resultant designs are based on whether we aim to minimize mission ramp weight or mission empty weight. Prof. Merret showed us how when analyzing some aircraft designs it becomes clear what the designers were 'optimizing' for. For instance, when analyzing the design of the G350 using a sizing code, it is clear they were trying to minimize empty weight, since cost is intrinsically linked to empty weight.

My main takeaway from this sizing project is that aircraft design is more complicated than it initially seems. It's very easy to say that we could just make aircraft more efficient if we used wings with higher aspect ratios or thinner airfoils, but there are often far more engineering trade-offs that are occuring in the background. This inspires my research into Multidisciplinary Optimization (MDO) and how it can be used in aircraft sizing problems, since there are intricate relationships between all parameters on an aircraft that an engineer has to be able to weigh to produce the right design for the right mission.

Apologies for how text-heavy this article has been. Not many shiny images unfortunately. You can download my sizing code 
