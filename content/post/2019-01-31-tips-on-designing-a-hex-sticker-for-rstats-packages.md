---
title: 'Tips on designing hex stickers for #rstats packages'
author: Hao
date: '2019-01-31'
slug: tips-on-designing-a-hex-sticker-for-rstats-packages
categories:
  - R
tags:
  - design
  - R
  - ideas
---

Earlier today on twitter, [Eric](https://twitter.com/theRcast) asked me this question

{{< tweet 1091035997104676871 >}}

Immediately after I replied I was using SketchApp, I realized he might be asking me about the actual "design workflow". On this aspect, although I feel like I'm not the best person to say this but I did gain some experience through making the following 5 stickers. Now let me try to organize the thoughts and put them down. 

<img src="/post/2019-01-31-tips-on-designing-a-hex-sticker-for-rstats-packages_files/tinytex.png" alt="tinytex" width="16%" style="display: inline-block;"/>
<img src="/post/2019-01-31-tips-on-designing-a-hex-sticker-for-rstats-packages_files/arduinor.png" alt="arduinor" width="16%" style="display: inline-block;"/>
<img src="/post/2019-01-31-tips-on-designing-a-hex-sticker-for-rstats-packages_files/kableExtra_sm.png" alt="kableExtra" width="16%" style="display: inline-block;"/>
<img src="/post/2019-01-31-tips-on-designing-a-hex-sticker-for-rstats-packages_files/Nor&#39;eastR.png" alt="noreastr" width="16%" style="display: inline-block;"/>
<img src="/post/2019-01-31-tips-on-designing-a-hex-sticker-for-rstats-packages_files/memor.png" alt="memor" width="16%" style="display: inline-block;"/>



I'm not an artist and I guess my only "systematic" design training is to "seriously" read this [Dota 2 Workshop - Character Art Guide](https://support.steampowered.com/kb/9334-YDXV-8590/dota-2-workshop-character-art-guide) (yeah, I'm a useless dota2 player and my skill is really bad 😐), which was written to help guide community artists make clothes for heros. I mean although it sounds like a joke, the document itself is actually a very good Design 101 class. It mentioned quite a few points that might seem to be too basic to designer but good for me at least. Also, the copy rights of all the screenshots that have monster-ish things belong to Valve.


## Selection of Colors
On the aspect of color picking, the dota2 doc tells me I should not pick more than 3 colors. "Less is more" it says.

<img src="/post/2019-01-31-tips-on-designing-a-hex-sticker-for-rstats-packages_files/dota2_art.png" alt="dota2 art guide" width="100%"/>

I think this point is critically important when we do design on small places like stickers. In most cases, a mixture of too many kinds of color is just not a good idea (Tidyverse itslef is a collection of many kinds so I'm not discussing the design of that sticker here). In fact, if you check the design of all rstudio's official stickers, you will find in many cases, they even only have 2 colors. 

<img src="/post/2019-01-31-tips-on-designing-a-hex-sticker-for-rstats-packages_files/rstudio-stickers.jpg" alt="" width="100%"/>

If you are looking for an example with 3 colors, `ggplot2` is a good example of combine the signature "ggplot gray" with black and blue on the aspect of color selection. 

<img src="/post/2019-01-31-tips-on-designing-a-hex-sticker-for-rstats-packages_files/hex-ggplot2.png" alt="" width="30%"/>

## Focus on the Package Identity
If you have tried to read that dota2 design doc, you will find it was reiterating the importance of "hero identity" again and again. The same rules applies to sticker design. When you are trying to come up with an hex-shaped image, the easiest routine is to think about what makes the package unique and if there are any good ways to visualize this "identity".

<img src="/post/2019-01-31-tips-on-designing-a-hex-sticker-for-rstats-packages_files/tinytex.png" alt="tinytex" width="30%"/>

In the `tinytex` example, when I was brainstorming the ideas on my commute, I immediately recognize the power of the word "tiny". How can we visualize the concept of "tiny" - a magnifier might do the job! That's how this design came up. 

## Package "Family" and Color Key Palettes

Heros in Dota2 have family. So they sometimes color heros with the same origin using the same color palettes.

<img src="/post/2019-01-31-tips-on-designing-a-hex-sticker-for-rstats-packages_files/dota2_family_color.png" alt="" width="50%"/>

R packages have "family" too. For example, my [kableExtra](https://github.com/haozhu233/kableExtra) package makes final tables in rmarkdown so it certainly blongs to the `rmarkdown` group. Since most of the stickers in this category are kind of "red-ish", I also gave this `kableExtra` sticker a red color background to allow it to fit into the family. 

<img src="/post/2019-01-31-tips-on-designing-a-hex-sticker-for-rstats-packages_files/rmarkdown.png" alt="" width="30%" style="display: inline-block;"/>
<img src="/post/2019-01-31-tips-on-designing-a-hex-sticker-for-rstats-packages_files/knitr.png" alt="" width="30%" style="display: inline-block;"/>
<img src="/post/2019-01-31-tips-on-designing-a-hex-sticker-for-rstats-packages_files/kableExtra_sm.png" alt="kableExtra" width="30%"/>

Another example is `dplyr`, `tidyr` and `broom`. Do you have a desire to use them together?

<img src="/post/2019-01-31-tips-on-designing-a-hex-sticker-for-rstats-packages_files/dplyr.png" alt="" width="30%" style="display: inline-block;"/>
<img src="/post/2019-01-31-tips-on-designing-a-hex-sticker-for-rstats-packages_files/tidyr.png" alt="" width="30%" style="display: inline-block;"/>
<img src="/post/2019-01-31-tips-on-designing-a-hex-sticker-for-rstats-packages_files/broom.png" alt="" width="30%"/>

## Software

Finally, as I said in my tweet, at least for me, [SketchApp](https://www.sketchapp.com/) is my go-to software to make these stickers (I'm not sure how rstudio folks made their stickers though). It offers many great functionalities for graphical design, such as adjusting the inner/outer width for polygons, setting up filling patterns and mask two layers together. Very good software. 


Again, thanks for reading my random thoughts! Keep in mind that the things you just read came from a design newbie like me so don't treat this post seriously. After all, if you have the ability to draw cute cats on paper, you don't need to worry about anything I just talked about. :P

<img src="/post/2019-01-31-tips-on-designing-a-hex-sticker-for-rstats-packages_files/purrr.jpg" alt="" width="30%"/>



