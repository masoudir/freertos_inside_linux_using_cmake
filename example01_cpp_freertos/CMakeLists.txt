cmake_minimum_required(VERSION 3.16)
project(freertos_inside_linux_example)


# Default to C99
if (NOT CMAKE_C_STANDARD)
    set(CMAKE_C_STANDARD 99)
endif ()

# Default to C++14
if (NOT CMAKE_CXX_STANDARD)
    set(CMAKE_CXX_STANDARD 14)
endif ()

if (CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
    add_compile_options(-W -Wall -Wextra -Wformat -Wmissing-braces -Wno-cast-align -Wparentheses -Wshadow -Wno-sign-compare -Wswitch -Wuninitialized -Wunknown-pragmas -Wunused-function -Wunused-label -Wunused-parameter -Wunused-value -Wunused-variable)
    #add_compile_options(-m32)
    add_compile_options(-DDEBUG=1 -g -UUSE_STDIO -D__GCC_POSIX__=1 -DMAX_NUMBER_OF_TASKS=300)
endif ()

set(CMAKE_CXX_FLAGS -pthread)

set(CMAKE_CXX_STANDARD 14)


# Include Cpp "include" directory
include_directories(include)
include_directories(src/include)
include_directories(src/portable/GCC/POSIX)
include_directories(/usr/include/x86_64-linux-gnu/)

add_executable(example_target1 main.cpp
        src/croutine.c
        src/event_groups.c
        src/list.c
        src/queue.c
        src/stream_buffer.c
        src/tasks.c
        src/timers.c
        src/portable/MemMang/heap_3.c
        src/portable/GCC/POSIX/port.c
        include/main.h)
