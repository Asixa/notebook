---
layout: research-note
title: "Fast R-CNN"
pdf: https://arxiv.org/pdf/1504.08083.pdf
location: https://arxiv.org/abs/1504.08083
info: ICCV 2015
excerpt: "Ross Girshick"
category: Literature-Review
area: "ai"
header:
  teaser: "assets/images/papers/fast-rcnn.png"

author_profile: false


toc: true
toc_sticky: true
show: true
related: false
read_time: false
showmeta: false
share: false
---
Girshick, Ross. "Fast r-cnn." Proceedings of the IEEE international conference on computer vision. 2015.

 
## First Pass

1. **Category**: 
2. **Context**: Related to R-CNN and SPPNet, and D-CNN.
3. **Correctness**:   
4. **Contributions**: Impovement in speed, accuracy and storage.
5. **Clarity**: Good.

what is **localization** in object detection?
{: .notice--info}

what is **fine-tuning** ?
{: .notice--info}

RCNN stand for Region-based Convolutional Neural Networks, 

## Introduction

<div class="mermaid">
graph TD;
    a["Deep ConvNet having some drawbacks"] --> a-2["why there are drawbacks for DCNN in genreal"];
    a-2["why there are drawbacks for DCNN in genreal"] --> b["R-CNN SPPnet's drawback"];
    b["R-CNN SPPnet's drawback"] --> c["Reasons for R-CNN and SPPnet's drawback"];
    c["Reasons for R-CNN and SPPnet's drawback"]--> d["Our contributions are we fixs their disadvantages"];
</div>

## Conclusion
1. what the paper have done
2. future work.