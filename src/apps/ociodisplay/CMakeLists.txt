find_package(OpenGL REQUIRED)
find_package(GLEW REQUIRED)
find_package(GLUT REQUIRED)
set(SOURCES
	main.cpp
)

add_executable(ociodisplay ${SOURCES})

if(NOT BUILD_SHARED_LIBS)
    target_compile_definitions(ociodisplay
        PRIVATE
        OpenColorIO_SKIP_IMPORTS
    )
endif()

target_include_directories(ociodisplay 
	SYSTEM
	PRIVATE
		${OPENGL_INCLUDE_DIR}
		${GLEW_INCLUDE_DIRS}
		${GLUT_INCLUDE_DIR}
)
target_link_libraries(ociodisplay
	PRIVATE 
		apputils
		openglbuilder
	PUBLIC
		OpenColorIO
		OpenImageIO
		${OPENGL_LIBRARIES}
		${GLEW_LIBRARIES}
		${GLUT_LIBRARIES}
)
install(TARGETS ociodisplay
	RUNTIME DESTINATION bin
)
