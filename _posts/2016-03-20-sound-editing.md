---
layout: post
title: Editing audio for iNaturalist documentation
tags: [audio]
---

We can document many species using the [Soundcloud](http://soundcloud.com) integration with [iNaturalist](http://www.inaturalist.org). And just like having clear photos for visual identification, we would like to have clear audio for identification.  But I haven't been able to find any good, simple explanations about how to go from a raw recording in the field to one ideal for confirming the identity of a species in the observation. This is an attempt at such a guide.

## Prerequisites

* _A recording._ Presumably, you've recorded identifiable sound(s) from an animal. The iPhone I use records in MP4 (.M4P) format

  - _Microphones can help._ I've recently gotten a [Rode VideoMic shotgun microphone](http://www.amazon.com/gp/product/B018KIJGU8?psc=1&redirect=true&ref_=oh_aui_detailpage_o00_s00) and am mostly really happy. It occasionally produces bad background noises, but I think that's because of the phone case interfering with a good plug-in.

* _Audio editing software._ There are lots of options, but I've been using [Audacity](http://www.audacityteam.org/) because it's open source, free, and appears to work well. There's a separate download required for importing MP4 files, but Audacity will prompt you to get the download.

* _Soundcloud account._ You'll need a [Soundcloud](http://soundcloud.com) account to link one or more recordings to an observation. An account is free for up to 180 minutes of uploaded audio.

## A walk-through

For this walk-through I'll be using [this recording](https://soundcloud.com/jacob-ogre/wbnu-20mar2016) of some [White-breasted Nuthatches](https://www.allaboutbirds.org/guide/White-breasted_Nuthatch/id) calling. Throughout we use the formatting `Menu -> Menu Item` or `Keyboard Shortcut` to describe commands.

### Part 1: Using the waveform

To start, use the `File -> Import` command to get the recording into Audacity. On import you should see something like this:

![_config.yml]({{ site.baseurl }}/images/posts/sound_editing/fig1.png)
*The basic interface of Audacity after importing the recording.*

The _waveform_ representation of the recording looks pretty non-descript, but we can zoom in by placing the cursor over the scale bar on the left of the image (which the shows a magnifying glass with a +) and clicking a few times:

![_config.yml]({{ site.baseurl }}/images/posts/sound_editing/fig2.png)
*The basic interface of Audacity after zooming in on the waveform.*

Now we can listen to the recording by clicking the play button or by pressing the `spacebar`. As the recording plays we can relate sounds to the waveform, with louder sounds at peaks, and background noise filling the center band.

One shortcoming you may witness is that the playback volume is probably really quiet. To solve that problem, we can use the `Effect -> Normalize` command:

![_config.yml]({{ site.baseurl }}/images/posts/sound_editing/fig3.png)

I've been normalizing to -0.05 dB:

![_config.yml]({{ site.baseurl }}/images/posts/sound_editing/fig4.png)

but you should try different options (and be ready to turn the volume down).

The first part of this recording has few or no bird calls, but a big noise spike:

![_config.yml]({{ site.baseurl }}/images/posts/sound_editing/fig5.png)
*We should just get rid of this part of the recording.*

We can select the part of the recording to remove (dark gray), then use `Edit -> Cut` or `Cmd + X` to delete it.

The waveform highlights some bad background sounds - those big peaks - still exist, and that we would like to tamp down:

![_config.yml]({{ site.baseurl }}/images/posts/sound_editing/fig6.png)
*The big spike is gone, but there are still too many noise peaks.*

Here we can use `Effect -> Click Removal` to wipe out the peaks. You may have to play with the settings a bit - and be prepared to `Edit - Undo` or `Cmd + Z` a few times - but you should end up with fewer clicks:

![_config.yml]({{ site.baseurl }}/images/posts/sound_editing/fig7.png)
*Now this is looking and sounding a bit better.*

Some isolated spikes are still in the waveform, but not near bird notes:

![_config.yml]({{ site.baseurl }}/images/posts/sound_editing/fig8.png)
*Still some spikes between bird calls...*

and we can use the cut command (`Cmd + X`) to just remove them:

![_config.yml]({{ site.baseurl }}/images/posts/sound_editing/fig9.png)
*...but these types of sections can just be snipped out.*

----

### Part 2: Using the spectrogram

This is about as far as I find the waveform useful. Now we want to switch to the _spectrogram_ view to see the frequencies of the background noise and the frequencies of the bird calls. To get there, choose the drop-down near the upper-left of the file viewing sub-window...

![_config.yml]({{ site.baseurl }}/images/posts/sound_editing/fig10.png)
*It took me a while to discover this.*

...and select `Spectrogram`...

![_config.yml]({{ site.baseurl }}/images/posts/sound_editing/fig11.png)

...which changes how the recording is shown:

![_config.yml]({{ site.baseurl }}/images/posts/sound_editing/fig12.png)
*The spectrogram is a rather different view than the waveform.*

Now we can see the nuthatch call notes as intense white patches from 1.5-3kHz (left scale). Some low-frequency spikes are visible along the bottom, and the general noise of the recording is all of the pink in the background. We can filter out the noise at frequencies higher and lower than calls to increase the intensity of the calls. The `Effect -> AUFilter` tool might work,

![_config.yml]({{ site.baseurl }}/images/posts/sound_editing/fig13.png)
*This is one option.*

if you know what you're doing...but I don't. Instead, I've been using `Effect -> AUHipass`

![_config.yml]({{ site.baseurl }}/images/posts/sound_editing/fig14.png)

to filter out the low-frequency noise, i.e., the high frequency sounds pass through. After setting the dot to a frequency below the low-end frequency of the call / song you want to keep, you can press 'Apply' multiple times to chip away at the noise from the bottom. Conversely, we can use `Effect -> AULowpass`

![_config.yml]({{ site.baseurl }}/images/posts/sound_editing/fig15.png)

to filter out the high-frequency noise. As with HiPass, you can 'Apply' multiple times to chip away, but from the high end. A complement to these is `Effect -> AUBandpass`, which allows keeping a band of frequencies.

![_config.yml]({{ site.baseurl }}/images/posts/sound_editing/fig16.png)

Last but not least there is the `AUGraphicEQ`, which, as the name suggests, provides a graphic equalizer for targeting particular frequency bands for amplification or suppression:

![_config.yml]({{ site.baseurl }}/images/posts/sound_editing/fig16b.png)
_The graphic equalizer shown here - which I didn't use for the nuthatch recording - is set for suppressing a band of noise in the 630-1200 Hz range._

After applying different filters, we should end up with a spectrogram that looks something like this:

![_config.yml]({{ site.baseurl }}/images/posts/sound_editing/fig17.png)
*Now we can much more clearly see and hear the nuthatches!*

Last but not least, we need to export the modified file under a new file name using `File -> Export Audio...`:

![_config.yml]({{ site.baseurl }}/images/posts/sound_editing/fig18.png)

----

## Uploading and linking

Now that we have a cleaned file (and the original; see below), we can upload to Soundcloud and link the files to an observation. The download interface is quite clean:

![_config.yml]({{ site.baseurl }}/images/posts/sound_editing/fig19.png)

You can edit the recording information as you see fit:

![_config.yml]({{ site.baseurl }}/images/posts/sound_editing/fig20.png)

Also be sure to edit the 'Metadata' tab to adjust the copyright as you see fit. Here I've made the recording [Creative Commons Attribution-ShareAlike](https://creativecommons.org/licenses/by-sa/3.0/us/).

![_config.yml]({{ site.baseurl }}/images/posts/sound_editing/fig21.png)

Now that it's uploaded, the clean file can be found [here](https://soundcloud.com/jacob-ogre/wbnu-20mar2016-clean).

-----------------------------------------------------------------------------------------------
_Optional ?_

I previously suggested (below) that it might be worth uploading both the original and the cleaned versions of files. [iNaturalist user @aredoubles](http://www.inaturalist.org/observations/aredoubles) noted that may not be necessary because we're not adjusting the tempo or frequency of the calls / songs. That's true, but I would add one caveat. One Audacity tool I didn't mention above, but have used, is `Noise Reduction`, which can affect the focal call / song. If `Noise Reduction`is used for bacground noise that occurs in the same frequency band as the target call / song then it might be worht uploading the original, too.

<del>__Note:__ Up until now I have been uploading just the best version of the recording. But as I've been writing this post I realized that it's probably better to include the clean version and the original. The primary reason is that I'm a novice at sound editing, and I don't know if I'm inadvertently modifying some part of the sound that shouldn't be modified. By placing the original in the record, someone with a lot more knowledge might be able to get a better recording that can be used in some sort of analysis, e.g., about bird song evolution.</del>
-----------------------------------------------------------------------------------------------

The last step is linking the Soundcloud files to the observation. In this case, I created a record using the iPhone app right after I made the recording. The recordings (original and clean) are available from the web interface, in the __Add media__ box in the upper-right corner of the page:

![_config.yml]({{ site.baseurl }}/images/posts/sound_editing/fig22.png)
*After checking the appropriate boxes be sure to save the edits!*

**Now the information needed to confirm an observation - a cleaned audio recording - [is available](http://www.inaturalist.org/observations/2810553).**

![_config.yml]({{ site.baseurl }}/images/posts/sound_editing/fig23.png)

----
**Upate 29 Mar 2016**

Added some clarifying text, an image of the graphic equalizer tool, and updated the note about uploading the original and clean versions of a recording. Thanks @aredoubles for the feedback!

