###############################################################################
#
# ftgl
# demo/CMakeLists.txt
#
# Howard N Smith (howard@blacktriangles.com)
# February 19, 2016
# (c) blacktriangles 2016 (http://www.blacktriangles.com)
###############################################################################

find_package( GLUT REQUIRED )

if( GLUT_FOUND )
  add_definitions( -DHAVE_GL_GLUT_H )
endif()

include_directories( ${ftgl_INCLUDE_DIR} ${CMAKE_CURRENT_LIST_DIR} ${GLUT_INCLUDE_DIR} )

## FTGLDemo ###################################################################
add_executable( ftgl_demo FTGLDemo.cpp tb.c trackball.c )
target_link_libraries(
    ftgl_demo
    PUBLIC
      ftgl
      ${GLUT_LIBRARY}
  )

## FTGLMFontDemo ##############################################################
add_executable( ftgl_mfont_demo FTGLMFontDemo.cpp tb.c trackball.c )
target_link_libraries(
    ftgl_mfont_demo
    PUBLIC
      ftgl
      ${GLUT_LIBRARY}
  )

## simple demo ################################################################
add_executable( simple_demo simple.cpp tb.c trackball.c )
target_link_libraries(
    simple_demo
    PUBLIC
      ftgl
      ${GLUT_LIBRARY}
  )