# FreeRTOS Blink
This project was generated in CubeMX following the [excellent FreeRTOS guide from Shawn Hymel](https://www.digikey.com/en/maker/projects/getting-started-with-stm32-introduction-to-freertos/ad275395687e4d85935351e16ec575b1). Most of the code here was generated via that tool. The only code modified was in [Core\Src\main.c](Core\Src\main.c). 

This project is self contained, it does not require any external SDKs etc.

For use in VS Code you will want the C++ and Makefile tools extensions. The [ARM GCC tools](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm) should be on the path.

On Windows you need make. The [GNU MCU Eclipse Windows Build Tools](https://gnu-mcu-eclipse.github.io/blog/2019/04/22/windows-build-tools-v2-12-20190422-released/) are a good choice. The instructions are for installing an xPack which is fine if the location is on the path. You can also find a zip that you can extract to a location of your choice on the [releases page](https://github.com/xpack-dev-tools/windows-build-tools-xpack/releases/tag/v2.12-20190422). 