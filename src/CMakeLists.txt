cmake_minimum_required(VERSION 3.16)
project(longscroll-qt LANGUAGES CXX)

include(../qt.cmake)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(QT NAMES Qt6 REQUIRED COMPONENTS Core)
find_package(Qt${QT_VERSION_MAJOR}
    REQUIRED
    COMPONENTS
        Core
        Gui
        Widgets
)
qt_standard_project_setup()

set(PROJECT_HEADERS
    contentiteminfo.h
    contentwidget.h
    contentwidgetitemfactory.h
    imageinfowidget.h
    imageitemwidget.h
    imagewidget.h
    longscroll-qt_global.h
    longscroll-qt_qtincludes.h
    longscrollwidget.h
    navigatorwidget.h
    notifyablescrollcontentwidget.h
    notifyingscrollarea.h
)

set(PROJECT_SOURCES
    contentiteminfo.cpp
    contentwidget.cpp
    contentwidgetitemfactory.cpp
    imageinfowidget.cpp
    imageitemwidget.cpp
    imagewidget.cpp
    longscrollwidget.cpp
    navigatorwidget.cpp
    notifyablescrollcontentwidget.cpp
    notifyingscrollarea.cpp
)

set(PROJECT_FORMS
    imageinfowidget.ui
    navigatorwidget.ui
)

qt_add_library(${PROJECT_NAME} SHARED
    ${PROJECT_HEADERS}
    ${PROJECT_SOURCES}
    ${PROJECT_FORMS}
)

target_compile_definitions(${PROJECT_NAME} PRIVATE LONGSCROLLQT_LIBRARY)

# Set include directories: 
# - BUILD_INTERFACE: use parent source dir so examples can use #include <longscroll-qt/xxx.h>
# - INSTALL_INTERFACE: headers installed to include/longscroll-qt/
target_include_directories(${PROJECT_NAME}
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/..>
        $<INSTALL_INTERFACE:include>
)

target_link_libraries(${PROJECT_NAME}
    PUBLIC
        Qt::Core
        Qt::Gui
        Qt::Widgets
)

include(GNUInstallDirs)

# Install headers to include/longscroll-qt/
install(FILES ${PROJECT_HEADERS}
    DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/longscroll-qt
)

install(TARGETS ${PROJECT_NAME}
    EXPORT longscroll-qt-targets
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
)

# Export targets for find_package
install(EXPORT longscroll-qt-targets
    FILE longscroll-qt-targets.cmake
    NAMESPACE longscroll::
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/longscroll-qt
)

# Generate package config file for find_package
include(CMakePackageConfigHelpers)
write_basic_package_version_file(
    "${CMAKE_CURRENT_BINARY_DIR}/longscroll-qt-config-version.cmake"
    VERSION 2.0.0
    COMPATIBILITY AnyNewerVersion
)
configure_file(
    "${CMAKE_CURRENT_SOURCE_DIR}/longscroll-qt-config.cmake.in"
    "${CMAKE_CURRENT_BINARY_DIR}/longscroll-qt-config.cmake"
    @ONLY
)
install(FILES
    "${CMAKE_CURRENT_BINARY_DIR}/longscroll-qt-config.cmake"
    "${CMAKE_CURRENT_BINARY_DIR}/longscroll-qt-config-version.cmake"
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/longscroll-qt
)
