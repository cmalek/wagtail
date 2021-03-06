.. _image_renditions:

Generating renditions in Python
=====================================

Rendered versions of original images generated by the Wagtail ``{% image %}`` template tag are called "renditions",
and are stored as new image files in the site's ``[media]/images`` directory on the first invocation.

Image renditions can also be generated dynamically from Python via the native ``get_rendition()`` method, for example:

 .. code-block:: python

    newimage = myimage.get_rendition('fill-300x150|jpegquality-60')

If ``myimage`` had a filename of ``foo.jpg``, a new rendition of the image file called
``foo.fill-300x150.jpegquality-60.jpg`` would be generated and saved into the site's ``[media]/images`` directory.
Argument options are identical to the ``{% image %}`` template tag's filter spec, and should be separated with ``|``.

The generated ``Rendition`` object will have properties specific to that version of the image, such as
``url``, ``width`` and ``height``, so something like this could be used in an API generator, for example:

 .. code-block:: python

    url = myimage.get_rendition('fill-300x186|jpegquality-60').url

Properties belonging to the original image from which the generated Rendition was created, such as ``title``, can
be accessed through the Rendition's ``image`` property:

 .. code-block:: python

    >>> newimage.image.title
    'Blue Sky'
    >>> newimage.image.is_landscape()
    True

See also: :ref:`image_tag`
