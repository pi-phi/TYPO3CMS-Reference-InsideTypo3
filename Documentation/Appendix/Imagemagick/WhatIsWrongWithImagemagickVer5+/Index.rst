

.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. ==================================================
.. DEFINE SOME TEXTROLES
.. --------------------------------------------------
.. role::   underline
.. role::   typoscript(code)
.. role::   ts(typoscript)
   :class:  typoscript
.. role::   php(code)


What is wrong with ImageMagick ver. 5+?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- "combine" creates a transparent entry in GIF-files (or makes an
  alphachannel) when overlaying images. Ver 4.2.9 doesn't. This creates
  the problem that the giffiles are often transparent in dark areas.

- "combine" interprets masks reversely to the norm. This means that any
  mask must be negated before rendering.


**Compatilibity:**
""""""""""""""""""

**<= 4.2.9:**

\+ NO-LZW problem

\- Transparency BUG

\- Mask negate

**5-5.1.x:**

\- NO-LZW problem

\+ Transparency BUG

\- Mask negate

**5.2.x:**

\- NO-LZW problem

\+ Transparency BUG

\+ Mask negate

\+ Gaussian?

Version 5+ Seems to be very slow.

Version 5.2.3 in test had the following problems: Using such as
-sharpen and -blur was very slow compared to 4.2.9. Blurring was maybe
2 or three times slower. -sharpen couldn't be used at all at values
above like 10 or so (and I normally use 99). It resulted in operations
never carried out.

Gaussian blurring didn't seem to work well. I succeeded in passing
values of 15. There was an error if a passed "15x5" for example. High
Gaussian blur values didn't make any difference.


Response from ImageMagick developers
""""""""""""""""""""""""""""""""""""

**Bob Friesenhahn <bfriesen@simple.dallas.tx.us>**

::

   > The greatest problem at this point is, that version 5+ seems to be
   > very slow compared to ver4: Version 5.2.3 in test had the
   > following problems: Using such as -sharpen and -blur was very slow
   > compared to 4.2.9. Blurring was maybe 2 or three times slower.
   > -sharpen couldn't be used at all at values above like 10 or so. It
   > resulted in operations never carried out. Gaussian blurring didn't
   > seem to work well. I succeeded in passing values of 15. There was
   > an error if a passed "15x5" for example. High Gaussian blur values
   > didn't make any difference. Now, can this be true?
   
   Note that the form and range of the arguments has totally changed for
   -sharpen and -blur since 4.2.9.  I suspect that this may be related to
   the problem you are seeing.
   cristy@mystic.es.dupont.com
   
   Version 5 has changed significantly from version 4.  Version 4 had support
   methods for the command line utilities.  Version 5 has exported it's
   API for others to use directly rather than relying on the command line
   utilities.  The good news is that the new API has stabelized and it is
   unlikely you will see any changes to the API in the future (except for 
   additional API called, the existing API should not change except in
   exeptional circumstances).
   
   > problems: Using such as -sharpen and -blur was very slow compared to
   > 4.2.9. Blurring was maybe 2 or three times slower. -sharpen couldn't be
   > used at all at values above like 10 or so. It resulted in operations
   > never carried out.  Gaussian blurring didn't seem to work well. I
   > succeeded in passing values of 15. There was an error if a passed
   > "15x5" for example. High Gaussian blur values didn't make any
   > difference.  Now, can this be true?
   
   Version 5 uses a more sophisticated sharpen/blur algorithm.  The parameter
   has changed as well.  The best default value is just 0 which is an
   auto sharpen/blur value.
   
   > - "combine" creates a transparent entry in gif-files (or makes an
   > alphachannel) when overlaying images. Ver 4.2.9 doesn't. This creates
   > the problem that the giffiles are often transparent in dark areas.  -
   
   You can always get rid of transparency with the +matte option.
   
   > "combine" interprets masks reversely to the norm. This means that any
   > mask must be negated before rendering.
   
   Opacity has reversed from version 4 to accomodate the SDL API.
   
   > Please give me some insight in what I might do, why version 5 is so
   > slow for these operations.
   
   Version 5 may be slower in general because ImageMagick always shoots for
   quality over speed.

128


