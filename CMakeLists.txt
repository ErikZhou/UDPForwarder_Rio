cmake_minimum_required(VERSION 3.21)

project(UDPForwarder_Rio)

set(CMAKE_C_STANDARD 11)

if (MSVC)
    set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} /FORCE:Multiple")
endif()

add_definitions(-DRIOSOCKETS_DLL)
add_executable(UDPForwarder_Rio
        main.cpp
        deps/RioSockets/Source/riosockets.c
        deps/Argtable3/argtable3.c
)

if (NOT UNIX)
    target_link_libraries(UDPForwarder_Rio PRIVATE ws2_32)
    SET_TARGET_PROPERTIES(UDPForwarder_Rio PROPERTIES PREFIX "")
endif()