---
layout: post
title: "Dynamic Symmetry Overlay in Lightroom"
description: "Using custom Loupe overlays for dynamic symmetry compositions."
tags: [photography, dynamic symmetry, overlay, lightroom]
categories: [Photography]
---

I've been reading [composition books](http://www.amazon.com/Photographers-Eye-Composition-Design-Digital/dp/0240809343)
and blogs in an attempt to discover new ways to organize the frame. One of those ways that I'm
currently experimenting with is called [*dynamic symmetry*](https://en.wikipedia.org/wiki/Jay_Hambidge),
and is discussed extensively on [James Cowman's blog](http://www.leicacameramonkey.com/blog/rule-of-thirds-vs-dynamic-symmetry).

In this post, I'm exploring how to add the dynamic symmetry grid as a custom overlay in Lightroom.

# Lightroom Loupe Overlays

*At the time of writing, Lightroom CC is in version 2015.5.1 (1073342).*

Lightroom comes with several [crop guide overlays](https://lightroomtricks.com/crop-overlays), but
unfortunately the dynamic symmetry grid isn't part of them. Although there is no way at the time
of writing to customize the overlay grids, another feature can be exploited as a workaround:
[loupe overlays](http://blogs.adobe.com/richardcurtis/2014/10/17/creativefriday-using-an-image-to-overlay-the-loupe-view-in-lightroom/).

The original goal of this feature is to put an image in its context of use, such as adding all the
surrounding text of a magazine cover. You will find this under the View menu:

<figure class="center">
    <a href="/images/dynamic_symmetry_lightroom/lightroom_1.png"><img src="/images/dynamic_symmetry_lightroom/lightroom_1_crop.jpg" alt=""></a>
    <figcaption><a href="/images/dynamic_symmetry_lightroom/lightroom_1.png" title="The Loupe Overlay menu">The Loupe Overlay menu</a>.</figcaption>
</figure>

By creating a set of custom images, we can use this feature to our advantage to overlay a dynamic
symmetry grid, using the `Command + Option + O` shortcut to toggle it:

<figure class="center">
    <a href="/images/dynamic_symmetry_lightroom/lightroom_2.png"><img src="/images/dynamic_symmetry_lightroom/lightroom_2_crop.jpg" alt=""></a>
    <figcaption><a href="/images/dynamic_symmetry_lightroom/lightroom_2.png" title="Dynamic Symmetry Overlay">The Dynamic Symmetry overlay</a>.</figcaption>
</figure>

# Issues and limitations

At the time of writing, the feature is unfortunately super buggy, and seems to crash Lightroom only
minutes after being enabled for the first time.

Another minor problem is that loupe overlays doesn't follow the image orientation. In other words,
you need both a horizontal and vertical grid images and manually switch between the two.

# Download the overlay files

I created different flavors of the grid, for either light or dark lines, and horizontal or vertical
orientation:

- [Dynamic Symmetry - Dark](/images/dynamic_symmetry_lightroom/dynamic_symmetry_overlay_dark.png)
- [Dynamic Symmetry - Dark (vertical)](/images/dynamic_symmetry_lightroom/dynamic_symmetry_overlay_dark_vertical.png)
- [Dynamic Symmetry - Light](/images/dynamic_symmetry_lightroom/dynamic_symmetry_overlay_light.png)
- [Dynamic Symmetry - Light (vertical)](/images/dynamic_symmetry_lightroom/dynamic_symmetry_overlay_light_vertical.png)
