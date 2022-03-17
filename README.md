# strlcpy - A safer answer to strncpy() 

This repository contains a copy of Todd C. Miller's ``strlcpy()`` function, 
originally written for the OpenBSD project, as far as I understand.
``strlcpy()`` copies a string from one variable to the other, but it 
**guarantees** the destination string to be null-terminated, thus being more
reliable and safer than both standard ``strncpy()`` and ``strcpy()``.

I'm providing this code for everyone's convenience, with portability across
POSIX systems in mind. I remember having some trouble sourcing this back then 
from a _trustworthy_ source. Some projects using ``strlcpy()`` seem to have 
lost track of the true origins of the module and have modified its licensing 
and copyright notices. This module being over two decades old and quite popular 
makes me think those misattribution cases are due to the community losing track 
of where ``strlcpy()`` actually originated from, and not due to any kind of 
malice.

Usually, to get a copy of this function you'd take it from other projects or, 
worse, try writing your own version of it. Also, you'll find this function in 
modules that also include the lesser used ``estrlcpy()``, which just adds 
printing an error message to stderr. If it's the case that you don't want to 
have unused functions lying around dead in your source code, you'll be very 
likely to prefer a self-contained version like the one I'm providing you with 
here.

The version provided on this repository is 
[1.16,](https://cvsweb.openbsd.org/src/lib/libc/string/strlcpy.c?rev=1.16&content-type=text/x-cvsweb-markup)
according to OpenBSD's internal versioning of modules. The version string has 
been kept in ``strlcpy.c``. This is the most recent version at the time I 
sourced this module back and I am **not** guaranteeing keeping it up-to-date 
with upstream.

An OpenBSD-specific call to ``DEF_WEAK()`` at the end of the module has been
removed. This modification does not affect the behavior of ``strlcpy()`` in any 
means whatsoever, as it is related to how the function is defined within the 
OS's libc, as can be read 
[on OpenBSD's libc documentation.](https://cvsweb.openbsd.org/src/lib/libc/include/DETAILS?rev=1.1&content-type=text/x-cvsweb-markup)

Also, this repository provides a ready-to-use header file ``strlcpy.h`` for you
to use. This trivial header file was written from scratch.

## Usage

I think it's safe for me to assume that anyone interested in this module knows
how to embed a module and its header file into the source tree of their C
projects.

Be aware, though that ``strlcpy.h`` requires you to include the appropriate 
header file for defining ``size_t`` before including ``strlcpy.h`` into your 
own program.

Just as a reminder, the interface of ``strlcpy()`` reads as follows:

```C
/*
 * Copy string src to buffer dst of size dsize.  At most dsize-1
 * chars will be copied.  Always NUL terminates (unless dsize == 0).
 * Returns strlen(src); if retval >= dsize, truncation occurred.
 */
size_t strlcpy(char *dst, const char *src, size_t dsize);
```

## License

``strlcpy.c`` and its associated header file are published under the ISC 
License. See ``LICENSE`` file for copyright and license details.
