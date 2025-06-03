# == DO NOT EDIT THE FOLLOWING LINES for the Raspberry Pi Pico VS Code Extension to work ==
if(WIN32)
    set(USERHOME $ENV{USERPROFILE})
else()
    set(USERHOME $ENV{HOME})
endif()
set(sdkVersion 2.1.1)
set(toolchainVersion 14_2_Rel1)
set(picotoolVersion 2.1.1)
set(FAMILY "rp2040")
set(picoVscode ${USERHOME}/.pico-sdk/cmake/pico-vscode.cmake)
if (EXISTS ${picoVscode})
    include(${picoVscode})
endif()
# ====================================================================================
set(PICO_BOARD pico CACHE STRING "Board type")

cmake_minimum_required(VERSION 3.20)

include(${CMAKE_CURRENT_SOURCE_DIR}/../../../hw/bsp/family_support.cmake)

# gets PROJECT name for the example (e.g. <BOARD>-<DIR_NAME>)
family_get_project_name(PROJECT ${CMAKE_CURRENT_LIST_DIR})

project(${PROJECT} C CXX ASM)

# Checks this example is valid for the family and initializes the project
family_initialize_project(${PROJECT} ${CMAKE_CURRENT_LIST_DIR})

# Espressif has its own cmake build system
if(FAMILY STREQUAL "espressif")
  return()
endif()

add_executable(${PROJECT})

pico_generate_pio_header(${PROJECT} ${CMAKE_CURRENT_SOURCE_DIR}/src/i2s.pio)

# Example source
target_sources(${PROJECT} PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}/src/main.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/usb_descriptors.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/quirk_os_guessing.c
        ${CMAKE_CURRENT_SOURCE_DIR}/src/i2s.c
        )

# Example include
target_include_directories(${PROJECT} PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}/src
        )

target_link_libraries(${PROJECT} PUBLIC
    pico_stdlib
    hardware_i2c
    hardware_dma
    hardware_pio
    hardware_clocks
)

# Configure compilation flags and libraries for the example without RTOS.
# See the corresponding function in hw/bsp/FAMILY/family.cmake for details.
family_configure_device_example(${PROJECT} noos)