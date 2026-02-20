cmake_minimum_required(VERSION 3.14)
project(02_cpp_utils VERSION 1.0.0 LANGUAGES CXX)

include(FetchContent)
FetchContent_Declare(
    cpp_core
    GIT_REPOSITORY https://github.com/compilerNayan/cpp_core.git
)
FetchContent_MakeAvailable(cpp_core)

add_library(02_cpp_utils INTERFACE)

set_target_properties(02_cpp_utils PROPERTIES
    VERSION ${PROJECT_VERSION}
)

target_link_libraries(02_cpp_utils INTERFACE cpp_core)

target_include_directories(02_cpp_utils INTERFACE
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)

include(GNUInstallDirs)

install(TARGETS 02_cpp_utils
    EXPORT 02_cpp_utilsTargets
)

install(EXPORT 02_cpp_utilsTargets
    FILE 02_cpp_utilsTargets.cmake
    NAMESPACE 02_cpp_utils::
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/02_cpp_utils
)
