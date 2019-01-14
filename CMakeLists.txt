cmake_minimum_required(VERSION 3.5)
project(sshfs)

set(FUSE_USE_VERSION 33)

#add_subdirectory(compat)
add_executable(sshfs sshfs.c cache.c)
target_compile_definitions(sshfs PUBLIC
    FUSE_USE_VERSION=${FUSE_USE_VERSION}
    _REENTRANT 
    HAVE_CONFIG_H
    _FILE_OFFSET_BITS=64 
)

target_include_directories(sshfs PRIVATE
    "/usr/local/include/fuse3"
    "/usr/include/glib-2.0"
    "/usr/lib/x86_64-linux-gnu/glib-2.0/include"
)
target_link_libraries(sshfs
    glib-2.0
    fuse3
    pthread
)
