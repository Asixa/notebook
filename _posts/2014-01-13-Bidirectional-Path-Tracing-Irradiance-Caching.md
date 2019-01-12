---
title: "Using Bidirectional path tracing with Irradiance caching in EDXRay"
header:
  teaser: "/assets/images/bidir_irradiance_cache/image_1.jpg"
tags:
  - Ray Tracing
  - Rendering
---

Recently I have implemented irradiance caching in the renderer I have been independently developing, EDXRay. This enabled the renderer to synthesize noiseless images in a short amount of time.

<figure style="width: 46%" class="align-left">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/bidir_irradiance_cache/image_0.jpg" alt="">
  <figcaption>Cornell box scene renderer with Irradiance caching. In scenes only contain diffuse objects, this algorithm is particularly efficient.</figcaption>
</figure> 

<figure style="width: 46%" class="align-right">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/bidir_irradiance_cache/image_1.jpg" alt="">
  <figcaption>The same scene as the left one, with irradiance samples visualized. Samples distributions are clampled in screen space.</figcaption>
</figure> 

The error function follows [this work](http://www.tabellion.org/et/paper/). Irradiance samples are distributed evenly in screen space. My implementation allows me to flexibly integrator used to calculate irradiance. Currently it supports both the 2 GI integrators originally in EDXRay: path tracer and bidirectional path tracer. For scenes where lights can easily be reached by sampling path from the camera, path tracing would suffice. For scenes such as the one below, where the majority of lighting comes from indirect illumination, bidirectional path tracing can produce images that has much less artifacts. All the images shown in this post was rendered with Irradiance Caching, sample distribution clamped at 1.5x to 10x pixel area, and irradiance evaluation sample count is 4096.

<figure style="width: 46%" class="align-left">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/bidir_irradiance_cache/image_2.jpg" alt="">
  <figcaption>Light source is this scene is right below the ceiling, therefore hard to be sampled if tracing paths from camera, resulting a really blotchy image.</figcaption>
</figure> 

<figure style="width: 46%" class="align-right">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/bidir_irradiance_cache/image_3.jpg" alt="">
  <figcaption>The same scene as left, with irradiance evaluating with bidirectional path tracing, sample amount of samples used. Since light paths were sampled from the light source too, we can construct a light path more efficiently.</figcaption>
</figure> 

Additionally, because bidirectional path tracing (BDPT) with multiple importance sampling is much better at rendering caustics and unidirectional path tracing, therefore in scenes that contain specular objects, using bidirectional path tracing to evaluate irradiance would also be much more efficient than path tracing, as shown below.

<figure style="width: 46%" class="align-left">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/bidir_irradiance_cache/image_4.jpg" alt="">
  <figcaption>Path tracing is not efficient at handling caustics. Scenes with specular objects will be blotchy when using path tracing with irradiance caching.</figcaption>
</figure> 
<figure style="width: 46%" class="align-right">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/bidir_irradiance_cache/image_5.jpg" alt="">
  <figcaption>Same scene as left, bidirectional path tracing is more capable of handling specular objects.</figcaption>
</figure> 

I am quite happy with the result. And I personally haven't seen this rendering approach (evaluating irradiance with BDPT in irradiance cache) used in other renderers such as mitsuba, luxray. Probably because caustics can be handled even better by photon mapping. The image below was renderred with irradiance caching, even bidirectional path tracing was used to calculate irradiance, the caustics area below the glass ball still has blotchy artifacts. This is due to caustics is a special form of indirect light that changes quickly over the surface, thus making it not as suitable for interpolation.

<figure style="width: 484px" class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/bidir_irradiance_cache/image_6.jpg" alt="">
  <figcaption>Even bidirectional path tracing would fail to efficiently render the caustics below the glass sphere, due to it's not suitable for interpolation.</figcaption>
</figure> 

When BDPT is used with irradiance caching, it's essential that it has all kinds of path sampling techniques. Just like explicitly connecting light vertices to camera lens is important for rendering caustics in normal path tracing (because caustics can be sampled much more easily by light tracing), here connecting light vertices to irradiance sample location is also important to make the algorithm work efficiently.

The next step is to use gradient information of irradiance to do more accurate interpolation. I am also interested in implementing [this work](http://zurich.disneyresearch.com/~wjarosz/publications/schwarzhaupt12practical.html). They seem to be able to development a much efficient error metric.

Lastly, I will post one more image rendered with my irradiance cache integrator, also 4096 bidirectional path samples were used to get irradiance samples. Just for fun, I also did another rendering just visualizing the indirect lighting in the same scene.

{% include figure image_path="/assets/images/bidir_irradiance_cache/image_7.jpg" alt="" caption="Sponza scene renderer with irradiance caching, 5000 path tracing samples used at each irradiance sample location." %}{: .align-center }
{% include figure image_path="/assets/images/bidir_irradiance_cache/image_8.jpg" alt="" caption="Same image as above, also showing the interpolated indirect lighting." %}{: .align-center }




