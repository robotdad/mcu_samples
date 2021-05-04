# CROSS COMPILER SETTING
SET(CMAKE_SYSTEM_NAME Generic)
# CMake 3.20 reports compiler information used by the IDE
cmake_minimum_required(VERSION 3.20 FATAL_ERROR)

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

project(freertos_hello)

set(MCUX_SDK_PROJECT_NAME freertos_hello.elf)

include(flags.cmake)
include(config.cmake)

add_executable(${MCUX_SDK_PROJECT_NAME} 
"freertos_hello.c"
"pin_mux.c"
"pin_mux.h"
"FreeRTOSConfig.h"
"board.c"
"board.h"
"clock_config.c"
"clock_config.h"
)

target_include_directories(${MCUX_SDK_PROJECT_NAME} PRIVATE
    ${ProjDirPath}
)

set(CMAKE_MODULE_PATH
    ${NXP_SDK_PATH}/devices/MK64F12/drivers
    ${NXP_SDK_PATH}/rtos/freertos
    ${NXP_SDK_PATH}/devices/MK64F12/utilities
    ${NXP_SDK_PATH}/devices/MK64F12
    ${NXP_SDK_PATH}/components/uart
    ${NXP_SDK_PATH}/components/serial_manager
    ${NXP_SDK_PATH}/components/lists
    ${NXP_SDK_PATH}/CMSIS/Include
)

# include modules
include(driver_port_MK64F12)

include(driver_gpio_MK64F12)

include(driver_clock_MK64F12)

include(middleware_freertos-kernel_heap_4_MK64F12)

include(driver_flash_MK64F12)

include(utility_debug_console_MK64F12)

include(driver_uart_MK64F12)

include(driver_smc_MK64F12)

include(device_MK64F12_CMSIS_MK64F12)

include(component_uart_adapter_MK64F12)

include(component_serial_manager_MK64F12)

include(driver_common_MK64F12)

include(component_lists_MK64F12)

include(component_serial_manager_uart_MK64F12)

include(device_MK64F12_startup_MK64F12)

include(utility_assert_MK64F12)

include(CMSIS_Include_core_cm4_MK64F12)

include(CMSIS_Include_common_MK64F12)

include(CMSIS_Include_dsp_MK64F12)

include(middleware_freertos-kernel_MK64F12)

include(middleware_freertos-kernel_extension_MK64F12)

include(utilities_misc_utilities_MK64F12)

include(device_MK64F12_system_MK64F12)


TARGET_LINK_LIBRARIES(${MCUX_SDK_PROJECT_NAME} PRIVATE -Wl,--start-group)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE m)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE c)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE gcc)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE nosys)

TARGET_LINK_LIBRARIES(${MCUX_SDK_PROJECT_NAME} PRIVATE -Wl,--end-group)