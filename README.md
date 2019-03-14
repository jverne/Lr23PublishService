# Lr23PublishService
A Lightroom Publish Service for 23 Photo Sharing

## Please note
**I am placing this on GitHub if anyone wants to run with it. I no longer maintain it, and
I rarely use 23 as a photo sharing service anymore.** The rest of this README is provided for
hysterical raisins. The plugin _should_ continue to work with Lr 5.

## What is this thing?

This document briefly discusses the Lightroom export publish service for
23. Lightroom is the premier raw photo management tool from Adobe, and
[23 is an excellent photo sharing site](http://23hq.com).

Adobe provides a reasonably complete SDK to create your own publish
services. Since no one else has created one for 23, I decided to do it
myself. This plug-in will only work with Lightroom 3 or higher. I have no
plans to recreate it for any other release of Lightroom.

The 23 Publish Service plug–in is based on the Flickr example code. It can
be consider beta quality. i.e., it is minimally tested, and may fail
spectacularly in some cases. It should not corrupt anything other than
its own connection to 23. That is, if something goes terribly awry, you
might have to republish your photos by hand in a less than ideal manner,
or be forced to "reset" your collection in some manner.

It should also be noted that I provide no warranty or guarantee
of fitness or correctness. For all I know, some rare combination of
Lightroom and OS on your computer could result in some disastrous
situation where all the photos in your main catalogue now have
handlebar moustaches. While highly unlikely, please use at your own
risk. And careful with that moustache wax.

Hey, it works for me!

It should be clear from the context, but I should state clearly that I
am *not* affiliated with 23 Photo Sharing in any official manner, other than
being a "Plus" user for a few years. I'm doing this only for fun and to be
a good 23 neighbour. I should give a shout-out to everyone on Team 23, but
especially Steffen for responding so quickly to API issues uncovered
during development.

23 Photo Sharing branding and icons are used by permission. Please don't
steal these!

## How do you use it?

The plug–in is delivered as a single zipfile containing this README and the `23PublishService.lrplugin` package.

Just place the 23PublishService.lrplugin package into the usual place
you put Lightroom plug–ins, [as described by Adobe](http://help.adobe.com/en_US/Lightroom/3.0/Using/WSB8C2DF2B-2ED0-4b97-BA18-5DBEDC69E7D9.html)

Remember that the plug–in package is actually a directory structure, so
copy the whole thing as one piece. The Finder/Explorer should do this
correctly, but other tools may not.

I put my export plug–ins on a Mac here:
`~/Library/Application Support/Adobe/Lightroom/Plugins`

I assume Windows folks have a similarly useful place for this stuff.

Once you load the plug–in via the Plug-in Manager, you can use the Publish
Services panel to create collections that can be published automatically
to 23. Please consult the
[Lightroom documentation on how to do this](http://help.adobe.com/en_US/Lightroom/3.0/Using/WS43660fa5a9ec95a81172e08124a15d684d-7ffe.html)

You can have multiple service definitions to 23, which correlate roughly to
Albums (or your main Photo "stream").

Note that this plug-in introduces custom metadata properties, which means
that the first time you use it, Lightroom will ask you to "update" the
database schema. This is normal and expected, and should happen only the
once. Occasionally, and upgrade to the plug-in may require another update
to the database schema.

## Who did this thing?

The 23 Photo Sharing publish service plug–in is created by [John D. Verne](http://clevermonkey.org),
from example code provided by Adobe.

## What if I need help?

I cannot offer any sort of real support. Ideally, you should raise questions and
make comments in the [23 API forum](http://www.23hq.com/photogroup/tech/conversation) even though that appears to be somewhat abondoned at this point.

If you are reporting a problem, be sure to explain the problem as clearly as you can and include details like the version of Lightroom and your operating system.

If you run into a problem and can't seem to get any help from anyone,
always check http://clevermonkey.org/Lightroom or the 23 Photo Sharing
Plug-in entry in the Lightroom Plug-in Manager for the latest release
and potential version information. Recent releases also have an
interface that allows checking for updates and looking at the release
change log from the Lightroom Plug-in Manager. _[This is no longer supported -- jdv]_

## What are some of the features?

The basic functionality is (I think) relatively complete, though I did
sweat a little over adding neat things like the ability to associate
service instances with Albums (including the ability to edit the Album
from Lightroom). I tried to make sure that bulk publish gestures would
not eat up system resources (thought the publish is still a
one-at-a-time operation, because 23 does not support the bulk upload
Flickr model).

Album details like the description and the Album cover photo can be set
from within Lightroom, and changes to Album descriptions on 23 will be
optionally accepted by the plug-in. Likewise, tag changes made on 23 
(or by another API call) will be preserved if a photo is republished.

I also wanted to be able to use the 23 publish status as metadata, so I
added basic metadata support.  Look in the Plugin metadata panel to see
what is there. I stole this idea from Jeffrey Friedl's publish plug–ins.
You should [buy plug–ins from Jeffrey]
(http://regex.info/blog/lightroom-goodies).

There is also a 23 Photo Sharing Extras interface in the Plug-in Extras
menu that provide functionality for marking "edited" photos as published
without having to upload/replace the photo on 23. (This is basic
functionality that I think is missing in Lightroom, so I added it as
a convenience.)  The same interface has a button to remove all this
plug–in specific metadata from selected photos.

**WARNING!** These two functions depend on a selection, but Lightroom always
has an implicit selection when switching to a collection, published or
otherwise. Be sure you know exactly what photos you are operating on. I
have tried to make this clear in the user interface, but it is something
you should be aware of.

You can check for updates to the plug-in via the Lightroom Plug-in Manager.
If there are new versions, you can go directly to the download link from
there. _[Update checks and auto-updates are no longer supported -- jdv]_

## What are the plans for the future?

I have a long list of improvements I'd like to make. Some of then are:

* Better debugging/logging mechanism.
* Nicer updating mechanism. Right now the update facility is a simple
  HTTP download.
* Photogroup support (this may require some API support tweaks on the
  part of 23).  
* Support associating existing photos on 23 with photos in your catalogue.
  This is a huge feature that is still in the very early planning stages.
* Basic localizations. (Probably on demand. If you want the plug–in in your
  language, I may ask you to provide translations!)

## Bugs

Probably. If you find something, let me know. I know there is at least one
threading bug if you publish a new photo while also republishing an
existing photo you might see an error. Dismissing the error dialogue and
selecting "Publish" should resolve this.
