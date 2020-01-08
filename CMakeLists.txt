cmake_minimum_required(VERSION 3.1)

project(DeepLabel)

set(CMAKE_CXX_STANDARD 14)

find_package(OpenCV REQUIRED)

find_package(Qt5 COMPONENTS Widgets Concurrent Sql REQUIRED)
# find_package(VTK REQUIRED)
# find_package(PCL 1.2 REQUIRED)

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)

# if(CMAKE_VERSION VERSION_LESS "3.7.0")
    set(CMAKE_INCLUDE_CURRENT_DIR ON)
# endif()

# include_directories (${PCL_INCLUDE_DIRS})
# link_directories    (${PCL_LIBRARY_DIRS})
# add_definitions     (${PCL_DEFINITIONS})

set (project_SOURCES
    QtAwesome/QtAwesome/QtAwesome.cpp
    QtAwesome/QtAwesome/QtAwesomeAnim.cpp
    src/main.cpp
    src/mainwindow.cpp
    src/labelproject.cpp
    src/imagelabel.cpp
    src/kittiexporter.cpp
    src/darknetexporter.cpp
    src/exportdialog.cpp
    src/multitracker.cpp
    src/baseexporter.cpp
    src/cocoexporter.cpp
    src/imagedisplay.cpp
    src/pascalvocexporter.cpp
    src/detection/detectoropencv.cpp
    src/detection/detectorsetupdialog.cpp
)

set (project_HEADERS  
    QtAwesome/QtAwesome/QtAwesome.h
    QtAwesome/QtAwesome/QtAwesomeAnim.h
    src/mainwindow.h
    src/labelproject.h
    src/imagelabel.h
    src/boundingbox.h
    src/kittiexporter.h
    src/darknetexporter.h
    src/exportdialog.h
    src/multitracker.h
    src/baseexporter.h
    src/cocoexporter.h
    src/imagedisplay.h
    src/pascalvocexporter.h
    src/detection/detectoropencv.h
    src/detection/detectorsetupdialog.h
)
set (project_FORMS
    src/mainwindow.ui
    src/exportdialog.ui
    src/imagedisplay.ui
    src/detection/detectorsetupdialog.ui
)

set (project_RESOURCES 
    QtAwesome/QtAwesome/QtAwesome.qrc
)
#set (VTK_LIBRARIES     vtkRendering vtkGraphics vtkHybrid QVTK)

#qt5_wrap_cpp      (project_HEADERS_MOC   ${project_HEADERS})
#qt5_wrap_ui       (project_FORMS_HEADERS ${project_FORMS})
qt5_add_resources (project_RESOURCES_RCC ${project_RESOURCES})

add_executable (deeplabel ${project_SOURCES} ${project_FORMS_HEADERS} ${project_RESOURCES_RCC})
target_link_libraries(deeplabel Qt5::Widgets Qt5::Concurrent Qt5::Sql)
target_link_libraries(deeplabel ${OpenCV_LIBS})
target_include_directories(deeplabel PRIVATE src)
target_include_directories(deeplabel PRIVATE QtAwesome/QtAwesome)
message("${OpenCV_INCLUDE_DIRS}")
target_include_directories(deeplabel PRIVATE ${OpenCV_INCLUDE_DIRS})
target_include_directories(deeplabel PRIVATE ${PROJECT_SOURCE_DIR})
# target_link_libraries (deeplabel ${PCL_LIBRARIES} ${VTK_LIBRARIES})