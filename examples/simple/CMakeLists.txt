cmake_minimum_required(VERSION 3.16)
project(simple LANGUAGES CXX)

include(../../qt.cmake)

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

qt_add_executable(${PROJECT_NAME} main.cpp)

target_link_libraries(${PROJECT_NAME}
    PRIVATE
        Qt::Core
        Qt::Gui
        Qt::Widgets
        longscroll-qt
)
