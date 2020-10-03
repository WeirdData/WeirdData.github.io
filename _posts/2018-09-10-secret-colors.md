---
author: Rohit Suratekar
avatar: rohit_suratekar.jpg
layout: post
title:  SecretColors - Make Plots Great Again !
date:   2018-09-10 13:00:00
categories: library
tags: python, colors, library
author_bio: Author is a computational biologist at NCBS, Bangalore.
author_twitter: rohitsuratekar
header_image: 2018-09-10-secret-colors/colors.jpg
---

> Update: New and updated version of this blog is now available [here](/2019/06/11/secret-colors-2.html).

I am obsessed with good colors. I particularly pay attention to all the colors I have used in my illustrations and graphics. This is extended to my data visualization also. There is huge amount of literature on how selecting correct colors impact your work <sup>[1](#ref1)</sup>. I recommend you to read one very old blog [Elegant Figures](https://earthobservatory.nasa.gov/blogs/elegantfigures/2013/08/05/subtleties-of-color-part-1-of-6/) by  Robert Simmon. This blog series not only talks about the basics of color theory but also the inspiration one should take to select colors for visualization. This blog post is all about colors and the inspiration behind my new `python` library [SecretColors](https://pypi.org/project/SecretColors/). For those who just want to check out library functions and comparison with `matplotlib` can skip the following section and can directly check out [next](#library).

### In search of good color palette
I was on the hunt for some good color palette. Obviously, every visualization is unique and need colors of its own. However, I was looking for some common colors which I can use in 'most' of my graphics and visualizations. I am no expert in the science of colors neither a good artist. It would take a lot of time for me to come up with a properly tested color palette. Hence I turned to existing color palettes which should provide me enough push to make my own. 
#### ColorBrewer
As mentioned in Robert's [blog](https://earthobservatory.nasa.gov/blogs/elegantfigures/2013/08/28/subtleties-of-color-part-5-of-6/), the first color palette I came across and was very popular [ColorBrewer](http://colorbrewer2.org/). Although many people already use this heavily, I kinda liked it initially and then quickly realized its limitations. This palette cum tool is perfect for some small visualization or simple plot. However, my personal opinion was that colors from this palettes are a little bit dull. Maybe this is because palette was originally designed for cartography and not for illustrations. Nonetheless, I still use this palette every once in a while especially when I have to print some illustrations. 
#### Google Material Design
I often create [mobile](https://github.com/rohitsuratekar) apps for personal and public use. I try to follow android app design guideline set up by Google<sup>[3](#ref2)</sup>. In addition to their guidelines on to structure your app, Google has been developing a new design language called [Material Design](https://material.io/design/). Immediately after reading about this, I started implementing its principles in my own apps. While reading this I stumble upon gold mine for colors Google [Material Design Color Palette](https://material.io/design/color/the-color-system.html). This palette changed my views about how one should select colors. I learned the concepts of primary, secondary and accent colors. Another most important thing I learned (and have implemented in my [SecretColors](https://pypi.org/project/SecretColors/) library) is that what text color I should use in the different color background.
#### IBM Design Language
I was using material design colors happily until I found out about [IBM Design Language](https://www.ibm.com/design/language/). I was in search of a perfect font (story for some other time) and found this design language. They have an entire section on colors. Once I saw IBM [color library](https://www.ibm.com/design/language/resources/color-library/), I knew this is the palette I was waiting for. This carefully color palette has colors for all kind of usage. This is my current vibrant goto color palette (until I find something better). 
 <a name = "library"></a>

### The SecretColors
Once I knew what kind of colors I wanted in my visualization, I just had to copy paste them into plotting library. Initially, I did not feel any difference but as projects diversified, I was spending unnecessary time going to websites, copy pasting hex values and then testing the plots. Finally, I decided to make my own library which should give me quick access to what I want. That is when this new library [SecretColors](https://pypi.org/project/SecretColors/) was born. 

I use `python` for most of my data analysis and visualization projects. I could go on telling you advantages of python over others but I think there are plenty of debates already existing on the internet <sup>[3](#ref2), [4](#ref3),  [5](#ref4)</sup>. In the end, the answer is, it is your choice and your convenience. Hence, the further article will only deal with python and it's plotting library `matplotlib` but colors used in this library are freely available and one can easily adapt them to use in their own analysis using any programming language. 

This library is Open Source and has released under MIT license. You can find all the code on its [GitHub](https://github.com/secretBiology/SecretColors) project and can compile your own. The library is available on PyPi and can be installed by the following command 


    pip3 install SecretColors  

<div><br></div>
This library only supports `Python 3+` and has a dependency (at least until version 0.0.3) on `random` and `warnings` which are shipped along with basic Python3 distribution. So essentially it should run without needing to install any new dependency. Basic usage and commands are provided on [GitHub](https://github.com/secretBiology/SecretColors) page. Here I will just compare it with inbuilt color palettes in `matplotlib`

### Comparison with basic plotting library

`matplotlib` provides very huge customization. This library is not providing any extra advantage to matplotlib. In fact, you can achieve **exact** same results by manually putting up color values. The main aim of this library to reduce time searching for colors and easy access to simple functions. In following plots I have used colors from matplotlib's default palette and from SecretColors's IBM palette. I have tried to use the same color grades for better comparison. Many of you might feel these are almost same colors but they are not :) Code used in following examples can be found in small [Gist](https://gist.github.com/rohitsuratekar/857678996d04a2d8e285f33a8ad4330a). 

|![Fig 1: Scatter](/assets/article_images/2018-09-10-secret-colors/scatter.png "scatter")|
|:--:|
|Fig 1: Scatter plot. Last gradient is changed by just passing one extra parameter.|

|![Fig 2: line](/assets/article_images/2018-09-10-secret-colors/line.png "line")|
|:--:|
|Fig 2: Line plot with default colors.|

|![Fig 3: histogram](/assets/article_images/2018-09-10-secret-colors/histogram.png "histogram")|
|:--:|
|Fig 3: Histogram with alpha values.|

|![Fig 4: heatmap](/assets/article_images/2018-09-10-secret-colors/heatmap.png "heatmap")|
|:--:|
|Fig 4: Heatmap with default options.|

|![Fig 5: bar](/assets/article_images/2018-09-10-secret-colors/bar.png "bar")|
|:--:|
|Fig 5: Bar graph with colors adjusted to respective value.|

|![Fig 6: bar2](/assets/article_images/2018-09-10-secret-colors/bar2.png "bar2")|
|:--:|
|Fig 6: Bar graph with default color cycle.|

### Final words 
This library is nowhere close to complete. A lot of functions needs to be added. However, already I am able to see the advantages of this library (at least in my data analysis). I have kept development open to all. Please feel free to provide feedback, suggestions or pull requests. 

### Other useful resources and tools
* [Adobe color CC](http://color.adobe.com/)
* [VMware Clarity Palette](https://vmware.github.io/clarity/documentation/v0.13/color)
* [Material UI Colors](https://www.materialui.co/)
* [W3 School Palette](https://www.w3schools.com/colors/colors_palettes.asp)
* [Apple Color Management](https://developer.apple.com/design/human-interface-guidelines/ios/visual-design/color/)
* [Paletton](http://paletton.com)
* [color-hex](http://www.color-hex.com/color-palettes/)

### References and Notes
1. <a name="ref1"></a> Elliot AJ. Color and psychological functioning: a review of theoretical and empirical work. Frontiers in Psychology. 2015;6:368. doi:10.3389/fpsyg.2015.00368.
2. <a name="ref2"></a> Google [Material Design](https://developer.android.com/guide/topics/ui/look-and-feel/) Principles 
3. <a name="ref3"></a> [Python vs (and) R for Data Science](https://blog.usejournal.com/python-vs-and-r-for-data-science-833b48ccc91d) by Brian Ray
4. <a name="ref4"></a> [MATLAB vs Python: for Scientific Computing — A Beginners Guide](https://medium.com/gradbunker/matlab-vs-python-for-scientific-computing-a-beginners-guide-a27f4dcbbc81) by Faisal Riyad
5. <a name="ref5"></a> [Dive Deep Into Python Vs Perl Debate – What Should I Learn Python or Perl?](https://www.tecmint.com/python-vs-perl-debate-what-should-i-learn-python-or-perl/) by Gunjit Khera
6. <a name="ref6"></a> I used 'SecretColors' as name to following nomenclature of my earlier venture of [SecretBiology](https://github.com/secretBiology).


Code used in the above analysis can be found [here](https://gist.github.com/rohitsuratekar/857678996d04a2d8e285f33a8ad4330a).

*(Header image is downloaded from Pixabay.com under CC0-license)*