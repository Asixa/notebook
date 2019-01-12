---
permalink: /talks/
title: "Behind the Pixels"
header:
  overlay_color: "#5e616c"
  overlay_image: /assets/images/Header1.jpg
  caption: 'Rendered with EDXRay'
excerpt: 'Computer Graphics and Deep Learning'
---

---

### Low Sample Count Ray Tracing with NVIDIA's Ray Tracing Denoisers
_SIGGRAPH 2018_

![](/assets/images/pages/SpeedofLight.jpg){: .align-left width="360px" }
In this session, Edward Liu from NVIDIA will demonstrate how state of the art denoising technologies provided in the Gameworks Ray Tracing module will make 1 sample per pixel ray tracing practical in many scenarios in real-time rendering, including area light shadows, ambient occlusion, glossy reflections and even indirect diffuse global illumination. Edward will show that one sample per pixel ray tracing with denoising can achieve much improved realism and fidelity when compared with traditional real-time rendering techniques. These denoisers have been successfully used in all the UE4 based cinematic real-time ray tracing demos released in 2018, including [Star Wars Reflections](https://www.youtube.com/watch?v=J3ue35ago3Y), Porsche 70th anniversary trailer [The Speed of Light](https://www.youtube.com/watch?v=Z85aPqqJzs0), Turing architecture launch [Project SOL](https://www.youtube.com/watch?v=KJRZTkttgLw&t=29s) and a few others.

[Video Recording](http://on-demand.gputechconf.com/siggraph/2018/video/sig1813-5-edward-liu-low-sample-count-ray-tracing-denoisers.html)

---

### Ray Tracing in Games with NVIDIA RTX
_Game Developers Conference 2018_

![](/assets/images/pages/RTX.jpg){: .align-left width="360px" }
NVIDIA will show how RTX, DXR along with GameWorks, Ray Tracing can revolutionize gaming by significantly boosting the real-time rendering quality as well as accelerating the content creating process.In particular, NVIDIA will show state of the art real-time denoising technologies from GameWorks that will drastically bring down the cost of ray traced rendering of area light soft shadows, ambient occlusions, and glossy reflections so they become practical for real-time rendering. In addition NVIDIA will showcase how RTX and DXR can be used to conveniently implement offline light transport algorithms like path tracing in your game engine, and show the power of that for content creation process. Finally NVIDIA will also provide some tips and guideline for integrating DXR into your engine, and discuss open challenges.

[Video Recording](https://www.gdcvault.com/play/1024813/), [Demo Video](https://www.youtube.com/watch?v=tjf-1BxpR9c)

---

### Cinematic Lighting in Unreal Engine
_GPU Technology Conference 2018_

![](/assets/images/pages/Reflections.jpg){: .align-left width="360px" }
Join Epic's Kim Libreri and Marcus Wassmer along with NVIDIA's Ignacio Llamas and Edward Liu as they provide an in-depth view of the creative and technical aspects of creating photo-realistic cinematic content that runs at real time.

Peek into the future of real-time computer graphics with “Reflections,” the first demonstration of real-time raytracing in Unreal Engine 4 using Microsoft’s new DXR framework and NVIDIA RTX technology for Volta GPUs. The Reflections demo illustrates the next-gen experimental lighting and rendering techniques in Unreal Engine, developed in collaboration with NVIDIA and ILMxLAB. 

[Demo Video](https://www.youtube.com/watch?v=J3ue35ago3Y)

---

### Accelerating your VR Games with VRWorks
_Game Developers Conference 2017_ and _GPU Technology Conference 2017_

![](/assets/images/pages/GDC17 VRWorks.jpg){: .align-left width="360px" }
Across graphics, audio, video, and physics, the NVIDIA VRWorks suite of technologies helps developers maximize performance and immersion for VR games and applications. This talk will explore the latest features of VRWorks, explain the VR-specific challenges they address, and provide application-level tips and tricks to take full advantage of these features. Special focus will be given to the details and inner workings of our latest VRWorks feature, Lens Matched Shading, along with the latest VRWorks integrations into Unreal Engine and Unity.

**Takeaway:** Attendees will gain an understanding of the unique challenges of real-time VR gaming and insight into the VRWorks suite of technologies.

[Video Recording](http://www.gdcvault.com/play/1024356/), [Slides](/assets/files/VRWorks_GDC17.pdf)

---

### High-Performance, Low-Overhead Rendering with OpenGL and Vulkan
_GPU Technology Conference 2016_


![](/assets/images/pages/Vulkan Talk.jpg){: .align-left width="360px" }
As advanced games and applications continue to push the performance envelope, developers look to their 3D APIs for improved predictability, threading and reduced CPU load. New extensions to OpenGL and a totally new 3D API Vulkan are answering these requests directly. This session introduces and details both of these approaches a shows how applications can use OpenGL "AZDO" (Approaching Zero Driver Overhead) extensions like NVIDIA's Command Lists to greatly reduce single-threaded CPU overhead while reusing existing OpenGL code. Going further, the second section introduces the new 3D API from Khronos called Vulkan. Finally, there is a discussion of the tradeoffs of extended OpenGL and AZDO versus Vulkan, and how a developer might choose between them.

[Video Recording](http://on-demand.gputechconf.com/gtc/2016/video/S6817.html), [Slides](/assets/files/High-performance, Low-Overhead Rendering with OpenGL and Vulkan - Edward Liu.pdf)