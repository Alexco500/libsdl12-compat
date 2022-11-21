# libsdl12-compat
Old SDL1.2 lib for macOS 10.13 or higher

This repository contains Xcode projects which will help you build the SDL1 Frameworks on modern macOS (10.13 or higher).
For that libsdl12-compat is used, which means you also need SDL2.Framework installed.

At the moment, the following SDL components are included

* SDL1 (SDL12-compat)
* SDL_image (v1.2.12)
* SDL_ttf (v2.0.11)

For better compatability, SDL_image is set to `SDL_IMAGE_USE_COMMON_BACKEND`, which means ImageIO is not used for loading images.
Instead libpng, libtiff, etc. are used and statically linked to the SDL libraries. 
The included binary dependencies are compiled as follows (both x86_64 and arm64, min macOS 10.13):

## brotli (1.0.9)
Nothing special, just configure
##lerc (4.0.0)
Provided Xcode project is used
##libpng (1.6.38)
`./configure  CFLAGS="-mmacosx-version-min=10.13 -arch x86_64 -arch arm64 -I/PATH/TO/libsdl12-compat/include" LDFLAGS="-mmacosx-version-min=10.13 -arch x86_64 -arch arm64 -L/PATH/TO/libsdl12-compat/libs"`
##freetype (2.12.1)
`./configure --with-harfbuzz=no --with-png=yes LIBPNG_CFLAGS="-I../libpng-1.6.38" LIBPNG_LIBS="-lpng16" --with-brotli=yes BROTLI_CFLAGS="-I../brotli-master/c/include" BROTLI_LIBS="-lbrotlicommon-static -lbrotlidec-static -lbrotlienc-static" CFLAGS="-mmacosx-version-min=10.13 -arch x86_64 -arch arm64" LDFLAGS="-mmacosx-version-min=10.13 -arch x86_64 -arch arm64 -L../brotli-master/ -L../libpng-1.6.38/.libs/"`
##libtiff (4.4.0)
`./configure --disable-jbig --disable-webp --with-x=no --with-lerc-include-dir=/PATH/TO/libsdl12-compat/include --with-lerc-lib-dir=/PATH/TO/libsdl12-compat/libs CFLAGS="-mmacosx-version-min=10.13 -arch x86_64 -arch arm64 -I/PATH/TO/libsdl12-compat/include" LDFLAGS="-mmacosx-version-min=10.13 -arch x86_64 -arch arm64 -L/PATH/TO/libsdl12-compat/libs"`
##xz (5.2.7)
`./configure --disable-doc --disable-lzma-links --disable-lzmadec --disable-lzmainfo --disable-nls --disable-scripts --disable-xzdec CFLAGS="-mmacosx-version-min=10.13 -arch x86_64 -arch arm64 -I/PATH/TO/libsdl12-compat/include" LDFLAGS="-mmacosx-version-min=10.13 -arch x86_64 -arch arm64 -L/PATH/TO/libsdl12-compat/libs"`

All includes are located in libsdl12-compat/include and the binaries are in libsdl12-compat/lib.


## Installation and Usage
Just put the SDL Frameworks into /System/Library/Frameworks or (prefered) into ~/Library/Frameworks. Also please install SDL2 Framework from the SDL project page at [https://www.libsdl.org/]()

If you want to use these Frameworks to port old SDL1 applications (like me :-)), you can simply include these into your application bundle (I always let Xcode do this for me). 

Keep in mind that the application should first link to SDL1, then to SDL2 to avoid linking issues.
