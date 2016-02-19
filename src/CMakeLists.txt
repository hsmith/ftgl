###############################################################################
#
# ftgl
# src/CMakeLists.txt
#
# Howard N Smith (howard@blacktriangles.com)
# February 19, 2016
# (c) blacktriangles 2016 (http://www.blacktriangles.com)
###############################################################################

## dependencies ###############################################################

find_package( Freetype REQUIRED )
find_package( OpenGL REQUIRED )
find_package( GLEW REQUIRED )
add_definitions( -DGLEW_STATIC )

if( UNIX )
  #hackasaurus rex
  get_filename_component( GLEW_LIB_DIR ${GLEW_LIBRARIES} DIRECTORY )
  set( GLEW_STATIC_LIB_PATH "${GLEW_LIB_DIR}/${CMAKE_STATIC_LIBRARY_PREFIX}GLEW${CMAKE_STATIC_LIBRARY_SUFFIX}" )

  add_library( glew STATIC IMPORTED )
  SET_TARGET_PROPERTIES(
      glew
        PROPERTIES
          IMPORTED_LOCATION ${GLEW_STATIC_LIB_PATH}
    )

  set( GLEW_LIBRARY glew )
endif()

## sources ####################################################################

file( GLOB_RECURSE
  ftgl_SOURCES
  ${CMAKE_CURRENT_LIST_DIR}
    *.cpp
  )

message( "ftgl_SOURCES:" ${ftgl_SOURCES} )

file( GLOB_RECURSE
  ftgl_HEADERS
  ${CMAKE_CURRENT_LIST_DIR}
    *.h
  )

set( ftgl_INCLUDE_DIR
      ${CMAKE_CURRENT_LIST_DIR}
      ${FREETYPE_INCLUDE_DIRS}
      ${OPENGL_INCLUDE_DIRS}
      ${GLEW_INCLUDE_DIRS}
      CACHE STRING "ftgl include directories"
  )

include_directories( 
    ${ftgl_INCLUDE_DIR}
  )

## library ####################################################################

add_library( ftgl ${ftgl_SOURCES} ${ftgl_HEADERS} )

target_link_libraries(
    ftgl
    PUBLIC
      ${FREETYPE_LIBRARIES}
      ${OPENGL_LIBRARIES}
      ${GLEW_LIBRARY}
  )