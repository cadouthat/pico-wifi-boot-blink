cmake_minimum_required(VERSION 3.13)

include(pico_sdk_import.cmake)

add_subdirectory(pico-wifi-boot)

project(pico_wifi_boot_blink_project C CXX ASM)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)
pico_sdk_init()

add_executable(main
  main.c
)

pico_enable_stdio_usb(main 1)
pico_enable_stdio_uart(main 0)

target_include_directories(main PRIVATE ${CMAKE_CURRENT_LIST_DIR} )

target_link_libraries(main
  pico_cyw43_arch_lwip_threadsafe_background
  pico_stdlib
  pico_wifi_boot
)

wifi_boot_user_program_bin(main)
