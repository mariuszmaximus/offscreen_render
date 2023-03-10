cmake_minimum_required(VERSION 3.0.0)
project(offscreen_render VERSION 0.1.0)


#make sure MOC compiler is called in parallel
set(CMAKE_AUTOGEN_PARALLEL AUTO)

# Find includes in corresponding build directories
set(CMAKE_INCLUDE_CURRENT_DIR ON)

# Instruct CMake to run moc automatically when needed.
set(CMAKE_AUTOMOC ON)

# Instruct CMake to create code from Qt resource files (*.qrc)
set(CMAKE_AUTORCC ON)

# UI ==> H generator from QT   # Instruct CMake to create code from Qt designer ui files
set(CMAKE_AUTOUIC ON)

set (BUILD_WITH_QT6 FALSE CACHE BOOL "Enable Qt6 support")
if (BUILD_WITH_QT6)
	set(QT_MIN_VERSION 6.0.0)
	set(QT_VERSION_BASE "Qt6")
else()
	set(QT_MIN_VERSION 5.14.0)
	set(QT_VERSION_BASE "Qt5")
endif()

# Find the QtWidgets library
find_package(${QT_VERSION_BASE} COMPONENTS Core Gui Widgets OpenGL Charts REQUIRED)


# The following define makes your compiler emit warnings if you use
# any feature of Qt which has been marked as deprecated (the exact warnings
# depend on your compiler). Please consult the documentation of the
# deprecated API in order to know how to port your code away from it.
# DEFINES += QT_DEPRECATED_WARNINGS
ADD_DEFINITIONS(-DQT_DEPRECATED_WARNINGS)

# You can also make your code fail to compile if you use deprecated APIs.
# In order to do so, uncomment the following line.
# You can also select to disable deprecated APIs only up to a certain version of Qt.
# DEFINES += QT_DISABLE_DEPRECATED_BEFORE=0x060000    # disables all the APIs deprecated before Qt 6.0.0
# ADD_DEFINITIONS(-DQT_DISABLE_DEPRECATED_BEFORE=0x060000)

add_executable(offscreen_render 
    fpscounter.cpp 
    glwidget.cpp 
    main.cpp 
    mainwindow.cpp 
    renderer.cpp 
    renderthread.cpp 
    sierpinski.cpp 
    texturebuffer.cpp

    mainwindow.ui
)

target_link_libraries(offscreen_render PRIVATE
    # Qt
	${QT_VERSION_BASE}::Widgets
	$<$<BOOL:${BUILD_WITH_QT6}>:${QT_VERSION_BASE}::OpenGLWidgets>
)

