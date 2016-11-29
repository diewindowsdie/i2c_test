cmake_minimum_required(VERSION 3.6)
project(cube2)

enable_language(ASM)

add_definitions(-DSTM32F100xB)

file(GLOB_RECURSE USER_SOURCES "Src/*.c")
file(GLOB_RECURSE HAL_SOURCES "Drivers/STM32F1xx_HAL_Driver/Src/*.c")

add_library(CMSIS
        Drivers/CMSIS/Device/ST/STM32F1xx/Source/Templates/system_stm32f1xx.c
        Drivers/CMSIS/Device/ST/STM32F1xx/Source/Templates/gcc/startup_stm32f100xb.s)

include_directories(Inc)
include_directories(Drivers/STM32F1xx_HAL_Driver/Inc)
include_directories(Drivers/CMSIS/Include)
include_directories(Drivers/CMSIS/Device/ST/STM32F1xx/Include)


add_executable(${PROJECT_NAME}.elf ${USER_SOURCES} ${HAL_SOURCES} ${LINKER_SCRIPT})

target_link_libraries(${PROJECT_NAME}.elf CMSIS)

set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -Wl,-Map=${PROJECT_SOURCE_DIR}/build/${PROJECT_NAME}.map")
set(HEX_FILE ${PROJECT_SOURCE_DIR}/build/${PROJECT_NAME}.hex)
set(BIN_FILE ${PROJECT_SOURCE_DIR}/build/${PROJECT_NAME}.bin)
add_custom_command(TARGET ${PROJECT_NAME}.elf POST_BUILD
        COMMAND ${CMAKE_OBJCOPY} -Oihex $<TARGET_FILE:${PROJECT_NAME}.elf> ${HEX_FILE}
        COMMAND ${CMAKE_OBJCOPY} -Obinary $<TARGET_FILE:${PROJECT_NAME}.elf> ${BIN_FILE}
        COMMENT "Building ${HEX_FILE} \nBuilding ${BIN_FILE}")













#


#set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
#
#set(SOURCE_FILES
#    Drivers/CMSIS/Device/ST/STM32F1xx/Include/stm32f100xb.h
#    Drivers/CMSIS/Device/ST/STM32F1xx/Include/stm32f1xx.h
#    Drivers/CMSIS/Device/ST/STM32F1xx/Include/system_stm32f1xx.h
#    Drivers/CMSIS/Device/ST/STM32F1xx/Source/Templates/system_stm32f1xx.c
#    Drivers/CMSIS/Include/arm_common_tables.h
#    Drivers/CMSIS/Include/arm_const_structs.h
#    Drivers/CMSIS/Include/arm_math.h
#    Drivers/CMSIS/Include/cmsis_armcc.h
#    Drivers/CMSIS/Include/cmsis_armcc_V6.h
#    Drivers/CMSIS/Include/cmsis_gcc.h
#    Drivers/CMSIS/Include/core_cm0.h
#    Drivers/CMSIS/Include/core_cm0plus.h
#    Drivers/CMSIS/Include/core_cm3.h
#    Drivers/CMSIS/Include/core_cm4.h
#    Drivers/CMSIS/Include/core_cm7.h
#    Drivers/CMSIS/Include/core_cmFunc.h
#    Drivers/CMSIS/Include/core_cmInstr.h
#    Drivers/CMSIS/Include/core_cmSimd.h
#    Drivers/CMSIS/Include/core_sc000.h
#    Drivers/CMSIS/Include/core_sc300.h
#    Drivers/STM32F1xx_HAL_Driver/Inc/Legacy/stm32_hal_legacy.h
#    Drivers/STM32F1xx_HAL_Driver/Inc/stm32f1xx_hal.h
#    Drivers/STM32F1xx_HAL_Driver/Inc/stm32f1xx_hal_cortex.h
#    Drivers/STM32F1xx_HAL_Driver/Inc/stm32f1xx_hal_def.h
#    Drivers/STM32F1xx_HAL_Driver/Inc/stm32f1xx_hal_dma.h
#    Drivers/STM32F1xx_HAL_Driver/Inc/stm32f1xx_hal_dma_ex.h
#    Drivers/STM32F1xx_HAL_Driver/Inc/stm32f1xx_hal_flash.h
#    Drivers/STM32F1xx_HAL_Driver/Inc/stm32f1xx_hal_flash_ex.h
#    Drivers/STM32F1xx_HAL_Driver/Inc/stm32f1xx_hal_gpio.h
#    Drivers/STM32F1xx_HAL_Driver/Inc/stm32f1xx_hal_gpio_ex.h
#    Drivers/STM32F1xx_HAL_Driver/Inc/stm32f1xx_hal_pwr.h
#    Drivers/STM32F1xx_HAL_Driver/Inc/stm32f1xx_hal_rcc.h
#    Drivers/STM32F1xx_HAL_Driver/Inc/stm32f1xx_hal_rcc_ex.h
#    Drivers/STM32F1xx_HAL_Driver/Inc/stm32f1xx_hal_tim.h
#    Drivers/STM32F1xx_HAL_Driver/Inc/stm32f1xx_hal_tim_ex.h
#    Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal.c
#    Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal_cortex.c
#    Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal_dma.c
#    Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal_flash.c
#    Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal_flash_ex.c
#    Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal_gpio.c
#    Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal_gpio_ex.c
#    Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal_pwr.c
#    Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal_rcc.c
#    Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal_rcc_ex.c
#    Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal_tim.c
#    Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal_tim_ex.c
#    Inc/main.h
#    Inc/stm32f1xx_hal_conf.h
#    Inc/stm32f1xx_it.h
#    Src/main.c
#    Src/stm32f1xx_hal_msp.c
#    Src/stm32f1xx_it.c)
#
#add_executable(cube2 ${SOURCE_FILES})