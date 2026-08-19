cmake_minimum_required(VERSION 3.13)

add_library(LiquidCrystalIO ../src/LiquidCrystalIO.cpp )

if (BUILD_FOR_STM32CUBE)
    target_compile_definitions(LiquidCrystalIO
            PUBLIC BUILD_FOR_STM32CUBE_CMAKE=1 IO_LOGGING_DEBUG=1
    )
else ()
    target_compile_definitions(LiquidCrystalIO
            PUBLIC BUILD_FOR_PICO_CMAKE=1 BUILD_PICO_FORCE_UART=1 IO_LOGGING_DEBUG=1
    )
endif ()

target_include_directories(LiquidCrystalIO PUBLIC
        ../src
)

target_link_libraries(LiquidCrystalIO PUBLIC IoAbstraction)
if(NOT BUILD_FOR_STM32CUBE)
    target_link_libraries(LiquidCrystalIO PUBLIC pico_stdlib pico_sync)
endif()
