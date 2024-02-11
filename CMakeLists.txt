cmake_minimum_required(VERSION 3.9)
project(imgui CXX)

set(CMAKE_CXX_STANDARD 11)

file(GLOB IMGUI_SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp)
add_library(imgui.imgui STATIC ${IMGUI_SOURCES})
target_include_directories(imgui.imgui PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
    $<INSTALL_INTERFACE:include/imgui>)
set_target_properties(imgui.imgui PROPERTIES OUTPUT_NAME imgui EXPORT_NAME imgui)
add_library(imgui::imgui ALIAS imgui.imgui)

install(
    FILES ${PROJECT_SOURCE_DIR}/imgui.h ${PROJECT_SOURCE_DIR}/imconfig.h
    DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/imgui)
install(
    TARGETS imgui.imgui
    EXPORT imgui
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    FRAMEWORK DESTINATION Library/Frameworks)
install(EXPORT imgui
    NAMESPACE imgui::
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/imgui
    FILE imgui.cmake)
