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
    ${NXP_SDK_PATH}/rtos/freertos
    ${NXP_SDK_PATH}/devices/MIMXRT685S/drivers
    ${NXP_SDK_PATH}/devices/MIMXRT685S
    ${NXP_SDK_PATH}/devices/MIMXRT685S/utilities
    ${NXP_SDK_PATH}/components/uart
    ${NXP_SDK_PATH}/boards/evkmimxrt685/flash_config
    ${NXP_SDK_PATH}/components/serial_manager
    ${NXP_SDK_PATH}/components/lists
    ${NXP_SDK_PATH}/CMSIS/Include
)

# include modules
include(middleware_freertos-kernel_cm33_nonsecure_port_MIMXRT685S_cm33)

include(driver_clock_MIMXRT685S_cm33)

include(middleware_freertos-kernel_heap_4_MIMXRT685S_cm33)

include(driver_common_MIMXRT685S_cm33)

include(driver_power_MIMXRT685S_cm33)

include(device_MIMXRT685S_CMSIS_MIMXRT685S_cm33)

include(utility_debug_console_MIMXRT685S_cm33)

include(utility_assert_MIMXRT685S_cm33)

include(component_usart_adapter_MIMXRT685S_cm33)

include(driver_flash_config_MIMXRT685S_cm33)

include(driver_flexspi_MIMXRT685S_cm33)

include(driver_cache_cache64_MIMXRT685S_cm33)

include(component_serial_manager_MIMXRT685S_cm33)

include(component_lists_MIMXRT685S_cm33)

include(component_serial_manager_uart_MIMXRT685S_cm33)

include(driver_flexcomm_usart_MIMXRT685S_cm33)

include(device_MIMXRT685S_startup_MIMXRT685S_cm33)

include(driver_flexcomm_MIMXRT685S_cm33)

include(driver_lpc_iopctl_MIMXRT685S_cm33)

include(driver_lpc_gpio_MIMXRT685S_cm33)

include(driver_reset_MIMXRT685S_cm33)

include(middleware_freertos-kernel_MIMXRT685S_cm33)

include(middleware_freertos-kernel_extension_MIMXRT685S_cm33)

include(CMSIS_Include_core_cm33_MIMXRT685S_cm33)

include(CMSIS_Include_common_MIMXRT685S_cm33)

include(CMSIS_Include_dsp_MIMXRT685S_cm33)

include(utilities_misc_utilities_MIMXRT685S_cm33)


TARGET_LINK_LIBRARIES(${MCUX_SDK_PROJECT_NAME} PRIVATE -Wl,--start-group)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE m)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE c)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE gcc)

target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE nosys)

TARGET_LINK_LIBRARIES(${MCUX_SDK_PROJECT_NAME} PRIVATE -Wl,--end-group)

ADD_CUSTOM_COMMAND(TARGET ${MCUX_SDK_PROJECT_NAME} POST_BUILD COMMAND ${CMAKE_OBJCOPY}
-Obinary ${PROJECT_BINARY_DIR}/${MCUX_SDK_PROJECT_NAME} ${PROJECT_BINARY_DIR}/sdk20-app.bin)

