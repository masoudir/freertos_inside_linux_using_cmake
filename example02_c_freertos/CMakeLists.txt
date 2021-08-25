cmake_minimum_required(VERSION 3.16)
project(freertos_for_gcc C)

set(CMAKE_C_STANDARD 99)


add_compile_options(-W -Wall -Wextra -Wformat -Wmissing-braces -Wno-cast-align -Wparentheses -Wshadow -Wno-sign-compare -Wswitch -Wuninitialized -Wunknown-pragmas -Wunused-function -Wunused-label -Wunused-parameter -Wunused-value -Wunused-variable -Wmissing-prototypes)
#add_compile_options(-m32)
add_compile_options(-DDEBUG=1 -g -UUSE_STDIO -D__GCC_POSIX__=1 -DMAX_NUMBER_OF_TASKS=300)

set(CMAKE_C_FLAGS -pthread)


include_directories(include)
include_directories(src/include)
include_directories(src/portable/GCC/POSIX)
#include_directories(/usr/include/x86_64-linux-gnu/)

add_executable(freertos_for_gcc_output_target main.c
        src/croutine.c
        src/event_groups.c
        src/list.c
        src/queue.c
        src/stream_buffer.c
        src/tasks.c
        src/timers.c
        src/portable/MemMang/heap_3.c
        src/portable/GCC/POSIX/port.c
        )
