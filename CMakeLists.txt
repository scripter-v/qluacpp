cmake_minimum_required( VERSION 3.15 )

project( qluacpp VERSION 1.0.0 )

add_library( qluacpp INTERFACE )

target_include_directories( qluacpp INTERFACE
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
)
