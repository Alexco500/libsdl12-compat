# libsdl12-compat
Old SDL1.2 lib for macOS 10.9 or higher

This repository contains Xcode projects which will help you build the SDL1 Frameworks on modern macOS (10.9 or higher).
For that libsdl12-compat is used, which means you also need SDL2.Framework installed. I used Xcode 14.0.1 for creating all frameworks and dependencies. If you search for a way to use more than one Xcode version, please try the excellent Xcodes app [GitHub link](https://github.com/RobotsAndPencils/XcodesApp)!

At the moment, the following SDL components are included

* SDL1 (SDL12-compat)
* SDL_net (v1.2.8)
* SDL_ttf (v2.0.11)
	* statically linked to libbrotli, libpng, libfreetype
* SDL_image (v1.2.12)
	* supports BMP, GIF, JPG, LBM, PCX, PNG, PNM, TGA, TIF, XCF, XPM, XV
	* statically linked to libtiff, libjpeg, libpng, liblzma, libLerc64
* SDL_mixer (v1.2.12)
	* supports CMD, WAV, MOD, MID, OGG, FLAC, MP3
	* statically linked to libogg, libvorbis, libvorbisfile, libFLAC, libmikmod and libmad


For better compatability, SDL\_image is set to `SDL_IMAGE_USE_COMMON_BACKEND`, which means ImageIO is not used for loading images.
Instead libpng, libtiff, etc. are used and statically linked to the SDL libraries. 
The included binary dependencies are compiled as follows (both x86_64 and arm64, min macOS 10.9, I always use \$HOME/test as prefix):

brotli (1.0.9)
---
To generate Autotools 'configure' file run './bootstrap'.

` ./configure CFLAGS="-mmacosx-version-min=10.9 -arch x86_64 -arch arm64 -I$HOME/test/include" LDFLAGS="-mmacosx-version-min=10.9 -arch x86_64 -arch arm64 -L/$HOME/test/lib" --prefix=$HOME/test --enable-shared=no`

lerc (4.0.0)
---
Provided Xcode project is used.

libpng (1.6.38)
---
`./configure  CFLAGS="-mmacosx-version-min=10.9 -arch x86_64 -arch arm64 -I$HOME/test/include" LDFLAGS="-mmacosx-version-min=10.9 -arch x86_64 -arch arm64 -L$HOME/test/lib" --prefix=$HOME/test --enable-shared=no`

freetype (2.12.1)
---
`./configure --with-harfbuzz=no --with-png=yes LIBPNG_CFLAGS="-I$HOME/test/include" LIBPNG_LIBS="-lpng16" --with-brotli=yes BROTLI_CFLAGS="-I$HOME/test/include" BROTLI_LIBS="-lbrotlicommon -lbrotlidec -lbrotlienc" CFLAGS="-mmacosx-version-min=10.9 -arch x86_64 -arch arm64" LDFLAGS="-mmacosx-version-min=10.9 -arch x86_64 -arch arm64 -L$HOME/test/lib" --prefix=$HOME/test --enable-shared=no`

libtiff (4.4.0)
---
`./configure --disable-jbig --disable-webp --with-x=no --with-lerc-include-dir=$HOME/test/include --with-lerc-lib-dir=$HOME/test/lib CFLAGS="-mmacosx-version-min=10.9 -arch x86_64 -arch arm64 -I$HOME/test/include" LDFLAGS="-mmacosx-version-min=10.9 -arch x86_64 -arch arm64 -L/$HOME/test/lib" CXXFLAGS="-mmacosx-version-min=10.9 -arch x86_64 -arch arm64 -I$HOME/test/include"   --prefix=$HOME/test --enable-shared=no`

xz (5.2.7)
---
` ./configure --disable-doc --disable-lzma-links --disable-lzmadec --disable-lzmainfo --disable-nls --disable-scripts --disable-xzdec CFLAGS="-mmacosx-version-min=10.9 -arch x86_64 -arch arm64 -I$HOME/test/include" LDFLAGS="-mmacosx-version-min=10.9 -arch x86_64 -arch arm64 -L$HOME/test/lib" --prefix=$HOME/test --enable-shared=no`

libogg (1.3.5)
---
`./configure CFLAGS="-mmacosx-version-min=10.9 -arch x86_64 -arch arm64" LDFLAGS="-mmacosx-version-min=10.9 -arch x86_64 -arch arm64"  --prefix=$HOME/test --enable-shared=no`

libvorbis (1.3.7)
---
`Use provided Xcode project`

libmikmod (3.3.11.1)
---
`Use provided Xcode project`

Flac (1.4.2)
---
` ./configure --disable-silent-rules --enable-static CFLAGS=-"mmacosx-version-min=10.9 -arch x86_64 -arch arm64" CXXFLAGS=-"mmacosx-version-min=10.9 -arch x86_64 -arch arm64" LDFLAGS="-mmacosx-version-min=10.9 -arch x86_64 -arch arm64" --with-ogg-libraries=$HOME/test/lib --with-ogg-includes=$HOME/test/include --prefix=$HOME/test --enable-shared=no`

All headers are located in libsdl12-compat/include and the binaries are in libsdl12-compat/lib.


## Installation and Usage
Just put the SDL Frameworks into /System/Library/Frameworks or (prefered) into ~/Library/Frameworks. Also please install SDL2 Framework from the SDL project page at [https://www.libsdl.org/]()

If you want to use these Frameworks to port old SDL1 applications (like me :-)), you can simply include these into your application bundle (I always let Xcode do this for me). 

Keep in mind that the application should first link to SDL1, then to SDL2 to avoid linking issues.
