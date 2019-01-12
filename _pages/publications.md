---
permalink: /publications/
title: "Behind the Pixels"
header:
  overlay_color: "#5e616c"
  overlay_image: /assets/images/Header1.jpg
  caption: 'Rendered with EDXRay'
excerpt: 'Computer Graphics and Deep Learning'
---

---

### Spatiotemporal Variance-Guided Filtering: Real-Time Reconstruction for Path-Traced Global Illumination

**Christoph Schied, Anton Kaplanyan, Chris Wyman, Anjul Patney, Chakravarty R. Alla Chaitanya, John Burgess, Shiqiu Liu, Carsten Dachsbacher, Aaron Lefohn, Marco Salvi**

_High Performance Graphics 2017 (Best Paper Award)_

![](/assets/images/pages/SVGF.jpg){: .align-left width="600px" }
We introduce a reconstruction algorithm that generates a temporally stable sequence of images from one path-per-pixel global illumination. To handle such noisy input, we use temporal accumulation to increase the effective sample count and spatiotemporal luminance variance estimates to drive a hierarchical, image-space wavelet filter [Dammertz et al. 2010]. This hierarchy allows us to distinguish between noise and detail at multiple scales using local luminance variance.
Physically based light transport is a long-standing goal for realtime computer graphics. While modern games use limited forms of ray tracing, physically based Monte Carlo global illumination does not meet their 30 Hz minimal performance requirement. Looking ahead to fully dynamic real-time path tracing, we expect this to only be feasible using a small number of paths per pixel. As such, image reconstruction using low sample counts is key to bringing path tracing to real-time. When compared to prior interactive reconstruction filters, our work gives approximately 10× more temporally stable results, matches reference images 5–47% better (according to SSIM), and runs in just 10 ms (± 15%) on modern graphics hardware at 1920×1080 resolution.

[Preprint](/assets/files/hpg17_svgf.pdf)


### Computer Simulations Imply Forelimb-Dominated Underwater Flight in Plesiosaurs

**Shiqiu Liu, Adam S. Smith, Yuting Gu, Jie Tan, C. Karen Liu and Greg Turk**

_PLoS Computational Biology_

![](/assets/images/pages/Underwater Plesiosaur High Res.jpg){: .align-left width="400px" }

Plesiosaurians are an extinct group of highly derived Mesozoic marine reptiles with a global distribution that spans 135 million years from the Early Jurassic to the Late Cretaceous. During their long evolutionary history they maintained a unique body plan with two pairs of large wing-like flippers, but their locomotion has been a topic of debate for almost 200 years. Key areas of controversy have concerned the most efficient biologically possible limb stroke, i.e whether it consisted of rowing, underwater flight, or modified underwater flight; and how the four limbs moved in relation to each other: did they move in or out of phase? Previous studies have investigated plesiosaur swimming using a variety of methods, including skeletal analysis, human swimmers, and robotics. We adopt a novel approach using a digital, three-dimensional, articulated, free-swimming plesiosaur in a simulated fluid. We generated a large number of simulations under various joint degrees of freedom to investigate how the locomotory repertoire changes under different parameters. Within the biologically possible range of limb motion, the simulated plesiosaur swims primarily with its forelimbs using an unmodified underwater flight stroke, essentially the same as turtles and penguins. In contrast, the hindlimbs provide relatively weak thrust in all simulations. We conclude that plesiosaurs were forelimb-dominated swimmers that used their hind limbs mainly for maneuverability and stability.

Full paper at [PLoS Computational Biology](http://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1004605).

Press Coverage:

1. [What Looks Like a Dinosaur But Swims Like a Penguin? It’s the Meyerasaurus.](http://www.usatoday.com/story/news/2015/12/17/meyerasaurus-dinosaur-swam-like-penguin/77507996/) _USA Today, 12/18/2015_
2. [Ancient Marine Reptiles Flew through the Water](http://www.livescience.com/53150-swimming-plesiosaurs.html) _Live Science, 12/18/2015_
3. [Plesiosaurs Literally Flew through Ocean](http://www.seeker.com/plesiosaurs-literally-flew-through-oceans-1770627747.html) _Discovery News, 12/17/2015_