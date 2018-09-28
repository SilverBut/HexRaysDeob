cmake_minimum_required(VERSION 3.12)
project(HexRaysDeob)

set(CMAKE_CXX_STANDARD 14)

#include_directories(.)

include_directories(./hexrays_sdk)
include_directories(./ida_sdk)

add_compile_definitions(__LINUX__=1)
add_compile_definitions(__EA64__=1)
add_compile_definitions(__X64__=1)

file(GLOB LIB_SOURCES
        AllocaFixer.cpp
        CFFlattenInfo.cpp
        DefUtil.cpp
        HexRaysUtil.cpp
        main.cpp
        MicrocodeExplorer.cpp
        PatternDeobfuscate.cpp
        PatternDeobfuscateUtil.cpp
        TargetUtil.cpp
        Unflattener.cpp
        )
file(GLOB LIB_HEADERS
        AllocaFixer.hpp
        CFFlattenInfo.hpp
        Config.hpp
        DefUtil.hpp
        HexRaysUtil.hpp
        MicrocodeExplorer.hpp
        PatternDeobfuscate.hpp
        PatternDeobfuscateUtil.hpp
        TargetUtil.hpp
        Unflattener.hpp
        )


add_library(HexRaysDeob_32 SHARED ${LIB_SOURCES} ${LIB_HEADERS})
add_library(HexRaysDeob_64 SHARED ${LIB_SOURCES} ${LIB_HEADERS})
target_compile_definitions(
        HexRaysDeob_32
        PRIVATE
        __EA64__=0 __X64__=0
)
target_compile_definitions(
        HexRaysDeob_64
        PRIVATE
        __EA64__=1 __X64__=1
)
