cmake_minimum_required(VERSION 3.13)
set(CMAKE_TOOLCHAIN_FILE ${CMAKE_CURRENT_SOURCE_DIR}/../../cmake/stm32_gcc.cmake)

project(stm32-blinky C ASM)
set(CMAKE_INCLUDE_CURRENT_DIR TRUE)
stm32_fetch_cmsis(H7)
stm32_fetch_cube(H7)
find_package(CMSIS COMPONENTS STM32H7_M7 REQUIRED)
find_package(HAL COMPONENTS STM32H7_M7 RCC GPIO CORTEX REQUIRED)

add_executable(stm32-blinky blinky.c stm32h7xx_hal_conf.h)
target_link_libraries(stm32-blinky
    HAL::STM32::H7::M7::RCC
    HAL::STM32::H7::M7::GPIO
    HAL::STM32::H7::M7::CORTEX
    CMSIS::STM32::H743ZI::M7
    STM32::NoSys 
)

