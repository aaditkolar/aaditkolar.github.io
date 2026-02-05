---
layout: page
title: GPU-Optimized Lattice-Boltzmann CFD Solver
img: assets/img/lbm_cover.jpg
importance: 1
category: work
related_publications: true
---

This project began as an attempt to evaluate the feasibility of Lattice-Boltzmann methods for higher resolution rotor wake modelling studies. Together with my advisor Prof. Matthew Clarke, I was to implement a Lattice-Boltzmann Method CFD solver using modern computational toolkits like Jax (and possibly Warp) to accelerate computation and provide automatic differentiation capabilities. We hoped to integrate this with <a href="https://www.rcaide.leadsresearchgroup.com/">RCAIDE</a> in the future to give users the option of higher fidelity aerodynamic analyses.

To write this code, I heavily utilized the textbook "The Lattice Boltzmann Method - Principles and Practice" {% cite lbm_kruger %}. It had excellent primers on the inner workings of LB methods that let me gain a fairly intuitive understanding of what I was doing. An LB method discretizes the domain into a set of grid points (i.e., a lattice). 

Particles 'stream' between grid points, with the probability of a particle travelling between 2 adjacent nodes defined in a "velocity set" for a certain grid architecture. After the 'streaming' step, the particles undergo a 'collision' step at each grid point, balancing out the velocities of the particles coming from different directions (as if they are colliding) before they repeat the cycle. This basic code uses the Bhatnagar-Gross-Krook collision operator, though more complex operators exist.

This is a fairly abstract explanation, so allow this GIF to explain this better (Ethan's entire article on Medium is great. He explains it much better than I do, if you have time to go read it):

<div class="col-sm-8 mx-auto">
    {% include figure.liquid loading="eager" path="assets/img/lbm_animation.gif" title="example image" class="img-fluid rounded z-depth-1" %}
</div>

<div class="caption">
    Animation of streaming-collision process in an LBM. <a href="https://medium.com/@ethan_38158/the-lattice-boltzmann-method-lbm-fluid-simulation-43a4fa248614">Source: Ethan Beddard</a>
</div>

<a href="https://youtu.be/ZUXmO4hu-20">This tutorial</a> by Felix Köhler on YouTube served as the basis for the 2D solver. A 3D solver was also built on similar principles. using  On larger grids, however, the solver's performance left something to be desired. Improving the performance of the solver required it to be just-in-time (JiT) compilable (a jax feature). This boils down an object not being allowed to mutate its own data members, which was a fairly straightforward modification in the end. 

Then, a jax foriloop is used in place of Python's for loops, allowing GPU/TPUs to anticipate computational demands in advance, producing a large speedup. The speedup was about 3x on a GPU and a massive 10x on a TPU, which is more specialized hardware. Some screenshots below:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/lbm1.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/lbm2.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/lbm3.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    From left to right, a simulation of a dense area of fluid diffusing into its surroundings
</div>

Unfortunately, the algorithm's memory usage was too high to simulate the grid sizes required to properly resolve a rotor wake at a viable hardware cost, resulting in the project being shelved for the time being. Nonetheless, this was an interesting dive into GPU-accelerated computing and how JiT code is written.
