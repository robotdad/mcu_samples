# CROSS COMPILER SETTING
SET(CMAKE_SYSTEM_NAME Generic)
# CMake 3.20 reports compiler information used by the IDE
CMAKE_MINIMUM_REQUIRED (VERSION 3.20 FATAL_ERROR)

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

# Not needed, let the output produce in default location extension uses
#SET(EXECUTABLE_OUTPUT_PATH ${ProjDirPath}/${CMAKE_BUILD_TYPE})
#SET(LIBRARY_OUTPUT_PATH ${ProjDirPath}/${CMAKE_BUILD_TYPE})


project(freertos_generic)

set(MCUX_SDK_PROJECT_NAME freertos_generic.elf)

include(flags.cmake)

include(config.cmake)

add_executable(${MCUX_SDK_PROJECT_NAME} 
"freertos_generic.c"
"pin_mux.c"
"pin_mux.h"
"FreeRTOSConfig.h"
"board.c"
"board.h"
"clock_config.c"
"clock_config.h"
"dcd.c"
"dcd.h"
)

target_include_directories(${MCUX_SDK_PROJECT_NAME} PRIVATE
    ${ProjDirPath}
)

set(CMAKE_MODULE_PATH
    ${NXP_SDK_PATH}/devices/MIMXRT1062/drivers
    ${NXP_SDK_PATH}/rtos/freertos
    ${NXP_SDK_PATH}/devices/MIMXRT1062
    ${NXP_SDK_PATH}/devices/MIMXRT1062/utilities
    ${NXP_SDK_PATH}/components/uart
    ${NXP_SDK_PATH}/components/serial_manager
    ${NXP_SDK_PATH}/components/lists
    ${NXP_SDK_PATH}/devices/MIMXRT1062/xip
    ${NXP_SDK_PATH}/boards/evkmimxrt1060/xip
    ${NXP_SDK_PATH}/CMSIS/Include
)

# include modules
include(driver_clock_MIMXRT1062)

include(middleware_freertos-kernel_heap_4_MIMXRT1062)

include(driver_common_MIMXRT1062)

include(device_MIMXRT1062_CMSIS_MIMXRT1062)

include(utility_debug_console_MIMXRT1062)

include(component_lpuart_adapter_MIMXRT1062)

include(component_serial_manager_MIMXRT1062)

include(component_lists_MIMXRT1062)

include(component_serial_manager_uart_MIMXRT1062)

include(driver_lpuart_MIMXRT1062)

include(device_MIMXRT1062_startup_MIMXRT1062)

include(driver_iomuxc_MIMXRT1062)

include(utility_assert_MIMXRT1062)

include(driver_igpio_MIMXRT1062)

include(driver_xip_device_MIMXRT1062)

include(driver_xip_board_MIMXRT1062)

include(middleware_freertos-kernel_MIMXRT1062)

include(middleware_freertos-kernel_extension_MIMXRT1062)

include(utilities_misc_utilities_MIMXRT1062)

include(CMSIS_Include_core_cm7_MIMXRT1062)

include(CMSIS_Include_common_MIMXRT1062)

include(CMSIS_Include_dsp_MIMXRT1062)

include(device_MIMXRT1062_system_MIMXRT1062)


TARGET_LINK_LIBRARIES(${MCUX_SDK_PROJECT_NAME} PRIVATE -Wl,--start-group)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE m)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE c)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE gcc)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE nosys)

TARGET_LINK_LIBRARIES(${MCUX_SDK_PROJECT_NAME} PRIVATE -Wl,--end-group)


