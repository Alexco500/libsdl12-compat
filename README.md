# libsdl12-compat
Old SDL1.2 lib for macOS 10.13 or higher (compat, needs SDL2 Framework)

The repository contains Xcode projects which will help you build SDL1 programs on modern macOS (10.13 or higher).
For that libsdl12-compat is used, which means you also need SDL2.Framework installed.

At the moment, the following SDL components are included
* SDL1 (SDL12-compat)
* SDL_image (v1.2.12)
* SDL_ttf (v2.0.11)

For better compatability, SDL_image is set to SDL_IMAGE_USE_COMMON_BACKEND, which means ImageIO is not used for loading images.
Instead libpng, libtiff, etc. are used. The included binary dependencies are compiled as follows
## brotli
Nothing special, just configure

##freetype
./configure --with-harfbuzz=no --with-png=yes LIBPNG_CFLAGS="-I../libpng-1.6.38" LIBPNG_LIBS="-lpng16" --with-brotli=yes BROTLI_CFLAGS="-I../brotli-master/c/include" BROTLI_LIBS="-lbrotlicommon-static -lbrotlidec-static -lbrotlienc-static" CFLAGS="-mmacosx-version-min=10.13 -arch x86_64 -arch arm64" LDFLAGS="-mmacosx-version-min=10.13 -arch x86_64 -arch arm64 -L../brotli-master/ -L../libpng-1.6.38/.libs/"

##libpng
./configure  CFLAGS="-mmacosx-version-min=10.13 -arch x86_64 -arch arm64 -I../../Xcode/SDL1_compat-Framework/include" 
LDFLAGS="-mmacosx-version-min=10.13 -arch x86_64 -arch arm64 
-L/Users/alexc/Source/Projekte/SDL1_Framework/Xcode/SDL1_compat-Framework/libs"

##libtiff
./configure --disable-jbig --disable-webp --with-x=no 
--with-lerc-include-dir=/Users/alexc/Source/Projekte/SDL1_Framework/Xcode/SDL1_compat-Framework/include 
--with-lerc-lib-dir=/Users/alexc/Source/Projekte/SDL1_Framework/Xcode/SDL1_compat-Framework/libs 
CFLAGS="-mmacosx-version-min=10.13 -arch x86_64 -arch arm64 -I../../Xcode/SDL1_compat-Framework/include" 
LDFLAGS="-mmacosx-version-min=10.13 -arch x86_64 -arch arm64 
-L/Users/alexc/Source/Projekte/SDL1_Framework/Xcode/SDL1_compat-Framework/libs"

##xz
 ./configure --disable-doc --disable-lzma-links --disable-lzmadec --disable-lzmainfo --disable-nls 
--disable-scripts --disable-xzdec CFLAGS="-mmacosx-version-min=10.13 -arch x86_64 -arch arm64 
-I../../Xcode/SDL1_compat-Framework/include" LDFLAGS="-mmacosx-version-min=10.13 -arch x86_64 -arch arm64 
-L/Users/alexc/Source/Projekte/SDL1_Framework/Xcode/SDL1_compat-Framework/libs"

##lerc-4.0.0
Provided Xcode project is used

