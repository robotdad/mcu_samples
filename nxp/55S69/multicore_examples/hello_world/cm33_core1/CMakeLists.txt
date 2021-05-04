# CROSS COMPILER SETTING
SET(CMAKE_SYSTEM_NAME Generic)
# CMake 3.20 reports compiler information used by the IDE
CMAKE_MINIMUM_REQUIRED (VERSION 3.20)

# THE VERSION NUMBER
SET (Tutorial_VERSION_MAJOR 1)
SET (Tutorial_VERSION_MINOR 0)

# ENABLE ASM
ENABLE_LANGUAGE(ASM)

SET(CMAKE_STATIC_LIBRARY_PREFIX)
SET(CMAKE_STATIC_LIBRARY_SUFFIX)

SET(CMAKE_EXECUTABLE_LIBRARY_PREFIX)
SET(CMAKE_EXECUTABLE_LIBRARY_SUFFIX)

# CURRENT DIRECTORY
SET(ProjDirPath ${CMAKE_CURRENT_SOURCE_DIR})

project(hello_world_cm33_core1)

set(MCUX_SDK_PROJECT_NAME hello_world_cm33_core1.elf)

include(flags.cmake)
include(config.cmake)

add_executable(${MCUX_SDK_PROJECT_NAME} 
"hello_world_core1.c"
"pin_mux.c"
"pin_mux.h"
"board.c"
"board.h"
"clock_config.c"
"clock_config.h"
)

target_include_directories(${MCUX_SDK_PROJECT_NAME} PRIVATE
    ..
)

set(CMAKE_MODULE_PATH
    ${NXP_SDK_PATH}/middleware/multicore
    ${NXP_SDK_PATH}/devices/LPC55S69/utilities/debug_console_lite
    ${NXP_SDK_PATH}/devices/LPC55S69/drivers
    ${NXP_SDK_PATH}/devices/LPC55S69
    ${NXP_SDK_PATH}/components/uart
    ${NXP_SDK_PATH}/components/lists
    ${NXP_SDK_PATH}/CMSIS/Include
    ${NXP_SDK_PATH}/devices/LPC55S69/utilities
)

# include modules
include(middleware_multicore_mcmgr_lpc55s69_LPC55S69_cm33_core1)

include(utility_debug_console_lite_LPC55S69_cm33_core1)

include(utility_assert_lite_LPC55S69_cm33_core1)

include(driver_mailbox_LPC55S69_cm33_core1)

include(driver_lpc_gpio_LPC55S69_cm33_core1)

include(middleware_multicore_mcmgr_LPC55S69_cm33_core1)

include(driver_lpc_iocon_LPC55S69_cm33_core1)

include(driver_common_LPC55S69_cm33_core1)

include(driver_power_LPC55S69_cm33_core1)

include(driver_reset_LPC55S69_cm33_core1)

include(driver_clock_LPC55S69_cm33_core1)

include(device_LPC55S69_CMSIS_LPC55S69_cm33_core1)

include(device_LPC55S69_startup_LPC55S69_cm33_core1)

include(driver_flexcomm_usart_LPC55S69_cm33_core1)

include(driver_flexcomm_LPC55S69_cm33_core1)

include(component_usart_adapter_LPC55S69_cm33_core1)

include(component_lists_LPC55S69_cm33_core1)

include(CMSIS_Include_core_cm33_LPC55S69_cm33_core1)

include(CMSIS_Include_common_LPC55S69_cm33_core1)

include(CMSIS_Include_dsp_LPC55S69_cm33_core1)

include(utilities_misc_utilities_LPC55S69_cm33_core1)

include(device_LPC55S69_system_LPC55S69_cm33_core1)


TARGET_LINK_LIBRARIES(${MCUX_SDK_PROJECT_NAME} PRIVATE -Wl,--start-group)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE m)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE c)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE gcc)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE nosys)

# STREQUAL is case sensitive
if(CMAKE_BUILD_TYPE STREQUAL Debug)
    target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE ${NXP_SDK_PATH}/devices/LPC55S69/gcc/libpower_soft.a)
endif()

if(CMAKE_BUILD_TYPE STREQUAL Release)
    target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE ${NXP_SDK_PATH}/devices/LPC55S69/gcc/libpower_soft.a)
endif()

TARGET_LINK_LIBRARIES(${MCUX_SDK_PROJECT_NAME} PRIVATE -Wl,--end-group)

ADD_CUSTOM_COMMAND(TARGET ${MCUX_SDK_PROJECT_NAME} POST_BUILD COMMAND ${CMAKE_OBJCOPY}
-Obinary ${PROJECT_BINARY_DIR}/${MCUX_SDK_PROJECT_NAME} ${PROJECT_BINARY_DIR}/core1_image.bin)

