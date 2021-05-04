# NXP Samples

These samples are from NXP SDKS. They have been modified so they can build outside of the NXP SDK directory. CMakeLists.txt has also been modified to exist in the root of the source rather than a subdirectory. The samples have been modified to build with Ninja rather than MinGW Makefiles. MinGW is not needed to build these samples.

ARMGCC_DIR must be set as an environemnt variable to the root of the installation, not bin, for the toolchain files to work. The variables NXP_SDK_PATH and CMAKE_TOOLCHAIN_FILE in .vscode/settings.json must be set to match your local install of the NXP SDK for the given board. 

As a toolchain is used to configure the compilers when prompted by CMake-Tools in VS Code for a kit you can choose "Unspecified".
