cmake_minimum_required(VERSION 3.13)

add_library(LiquidCrystalIO ../src/LiquidCrystalIO.cpp )

target_compile_definitions(IoAbstraction
        PUBLIC BUILD_FOR_PICO_CMAKE=1 BUILD_PICO_FORCE_UART=1 IO_LOGGING_DEBUG=1
)

target_include_directories(LiquidCrystalIO PUBLIC
        ../src
)

target_link_libraries(LiquidCrystalIO PUBLIC pico_stdlib pico_sync IoAbstraction)
