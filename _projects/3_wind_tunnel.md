---
layout: page
title: Flying Wing Concept Wind Tunnel Test
# description: a project with a background image and giscus comments
img: assets/img/tunnel_cover.png
importance: 1
category: work
---

As part of AE 460, the Aerodynamics Lab class at the University of Illinois, my 4 teammates and I were tasked with designing and testing a flying-wing concept aircraft for any commercial purpose. Using the <a href="https://www.zipline.com/africa">Zipline delivery drones in Africa</a> as inspiration, we decided to design a similar package delivery flying wing drone. 

One of the primary difficulties with designing a flying wing aircraft is achieving static stability, as cambered airfoils have a natural pitch-down tendency about their aerodynamic center. To achieve this, significant sweep and a twist profile were introduced to give the wing desirable stability derivatives by moving the neutral point rearwards: <a href="https://www.apogeerockets.com/education/downloads/Newsletter15.pdf">here is a page with some good info on how that works</a>

Here is the theoretical design in OpenVSP: 
<div class="col-sm-8 mx-auto">
    {% include figure.liquid loading="eager" path="assets/img/flyingwing_vsp.png" title="example image" class="img-fluid rounded z-depth-1" %}
</div>

AVL was used to estimate the aerodynamic properties of the aircraft, as I have generally found its aerodynamics solver to be more reliable than VSPAERO. It was used to determine an appropriate wing twist profile and generate theoretical results.

My teammate helped us take the OpenVSP model and turn it into a 3D-printable CAD model, with the necessary probe attachment point. Here is the result:
<div class="col">
    <div class="row justify-content-center">
        <div class="col-8">  <!-- col-6, col-4, etc. for smaller -->
            <div class="row-sm mt-3 mt-md-0">
                {% include figure.liquid loading="eager" path="assets/img/flyingwing_cad_sketch.png" title="example image" class="img-fluid rounded z-depth-1" %}
            </div>
            <div class="row-sm mt-3 mt-md-0">
                {% include figure.liquid loading="eager" path="assets/img/tunnel_cover.png" title="example image" class="img-fluid rounded z-depth-1" %}
            </div>
        </div>
    </div>
</div>

This model was tested in the wind tunnel at wind speeds of 25, 50 and 80 ft/s. The force probe was used to ascertain lift, drag and moment values, which we then analyzed. We found that our theoretical neutral point calculation was very accurate, though the drag values measured by the force probe were slighty suspect. Read the full report <a href="../../assets/pdf/design_lab.pdf">here</a>
