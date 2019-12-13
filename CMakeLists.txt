project(qtpropertybrowser)

cmake_minimum_required(VERSION 3.5)

include(GenerateExportHeader)

find_package(Qt5Core REQUIRED)
find_package(Qt5Gui REQUIRED)
find_package(Qt5Widgets REQUIRED)

# Instruct CMake to run moc automatically when needed.
set(CMAKE_AUTOMOC ON)

file(GLOB QTPROPERTYBROWSER_SOURCES src/qtpropertybrowser/*.cpp)
file(GLOB QTPROPERTYBROWSER_HEADERS src/qtpropertybrowser/*.h)

add_library(qtpropertybrowser SHARED ${QTPROPERTYBROWSER_SOURCES} ${QTPROPERTYBROWSER_HEADERS})
generate_export_header(qtpropertybrowser)

set_property(TARGET qtpropertybrowser PROPERTY WINDOWS_EXPORT_ALL_SYMBOLS ON)

target_link_libraries(qtpropertybrowser PRIVATE Qt5::Widgets)

target_include_directories(qtpropertybrowser INTERFACE src)
target_include_directories(qtpropertybrowser INTERFACE ${CMAKE_CURRENT_BINARY_DIR})

install(TARGETS qtpropertybrowser DESTINATION lib)
if(PREON_RPATH_SAMEDIR)
    set_target_properties(qtpropertybrowser PROPERTIES INSTALL_RPATH ${PREON_RPATH_SAMEDIR})
endif()
