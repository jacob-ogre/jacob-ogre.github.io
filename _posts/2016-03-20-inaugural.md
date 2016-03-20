---
layout: post
title: An inaugural post
categories: other
---

As with any such endeavor, we need an inaugural post to test the system out. Because this is all written in [markdown](https://daringfireball.net/projects/markdown/), I need to test out a few basic features.

1. This is the first point in an ordered list.
2. This is the second point.
    1. This is a sub-point.
    2. And this is a second.

We can write codeblocks:

```python
import sys

if len(sys.argv) != 3:
    print main.__doc__
    sys.exit()

main()
```

```r
library(ggplot2)

# If I had some data I would make a plot here...

ggplot(dat, aes(x, y)) +
    geom_jittter()
```

I will need or want to add images to posts (e.g., plots or photos), which means this should work:

![_config.yml]({{ site.baseurl }}/images/posts/inaugural/PA107229.JPG)
*Hopefully there's a photo of a monarch butterfly immediately above this.*

Oh, and I will need to embed `iframe`s sometimes, including [Soundcloud](http://soundcloud.com) recordings:

<iframe width="100%" height="450" scrolling="no" frameborder="no" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/251595089&amp;auto_play=false&amp;hide_related=false&amp;show_comments=true&amp;show_user=true&amp;show_reposts=false&amp;visual=true"></iframe>

And there _should_ be a player above.
