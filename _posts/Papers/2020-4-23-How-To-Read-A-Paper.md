---
layout: research-note
title: "How to Read a Paper"
pdf: https://web.stanford.edu/class/ee384m/Handouts/HowtoReadPaper.pdf
location: https://web.stanford.edu/class/ee384m/Handouts/HowtoReadPaper.pdf
info: stanford.edu
excerpt: ""
category: Literature-Review
area: "other"
header:
  teaser: "assets/images/papers/how-to-read-a-paper.png"

author_profile: false


toc: true
toc_sticky: true
show: true
related: false
read_time: false
showmeta: false
share: false
---

# Writing logic
<div class="mermaid">
graph TD;
    Three-Pass-Apporach -->First-pass;
    Three-Pass-Apporach -->Second-pass;
    Three-Pass-Apporach -->Third-pass;
    First-pass -->Literature-Survery;
    Second-pass -->Literature-Survery;
    Third-pass -->Literature-Survery;
</div>


# Summary
## Three-pass approach.
Read a paper in three passes.
1.  general idea.
2.  grasp paper’s content.
3.  depth and detail.

### First pass
Read abstract, intro, conclusion, and the section headers, also the references.
#### **Five-Cs**
1. ***Category***: \\
    What type of paper is this? \\
    A measurement paper? \\
    An analysis of an existing system? A\\
    description of a research prototype?
2. ***Context***: \\
Which other papers is it related to? \\
Which theoretical bases were used to analyze the problem?
3. ***Correctness***: Do the assumptions appear to be valid?
4. ***Contributions***: What are the paper’s main contributions?
5. ***Clarity***: Is the paper well written?

### Second Pass
Look at figures, diagrams,and check the unreaded references.
incomprehensible is ok.

### Third Pass
**Virtually re-implement** the paper.\\
Jot down ideas for furture work.\\
Find the strong and week point.

## Literature Survery
Doing a literature survery in three steps:
1.  Search keywords through Google Scholar.
2.  Find shared citations and repeated author names.
3.  look through the recent proceedings of the top conference in the area.


## References
1. [S. Peyton Jones, “Research Skills,”](http://research.microsoft.com/simonpj/Papers/givinga-talk/giving-a-talk.htm).
2.  [T. Roscoe, “Writing Reviews for Systems Conferences,”](http://people.inf.ethz.ch/troscoe/pubs/reviewwriting.pdf).
3. [H. Schulzrinne, “Writing Technical Articles,”](http://www.cs.columbia.edu/ hgs/etc/writingstyle.html).
4.  [G.M. Whitesides, “Whitesides’ Group: Writing a Paper,”](http://www.che.iitm.ac.in/misc/dd/writepaper.pdf).


