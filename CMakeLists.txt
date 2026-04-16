cmake_minimum_required(VERSION 3.19)
project(120fps-method LANGUAGES CXX)

find_package(Qt6 6.5 REQUIRED COMPONENTS Core Widgets Svg Multimedia)

qt_standard_project_setup()

qt_add_resources(QRC_FILES resources.qrc)

set(APP_RC_FILE "")
if(EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/file.rc")
    set(APP_RC_FILE file.rc)
endif()

qt_add_executable(120fps-method
    WIN32 MACOSX_BUNDLE
    main.cpp
    mainwindow.cpp
    mainwindow.h
    mainwindow.ui
    hovereventfilter.h
    ${APP_RC_FILE}
    ${QRC_FILES}
)

target_link_libraries(120fps-method
    PRIVATE
        Qt::Core
        Qt::Widgets
        Qt::Svg
        Qt::Multimedia
)

target_include_directories(120fps-method PRIVATE ${APP_ICON_DIR})

include(GNUInstallDirs)

install(TARGETS 120fps-method
    BUNDLE  DESTINATION .
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
)

qt_generate_deploy_app_script(
    TARGET 120fps-method
    OUTPUT_SCRIPT deploy_script
    NO_UNSUPPORTED_PLATFORM_ERROR
)
install(SCRIPT ${deploy_script})
