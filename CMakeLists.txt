cmake_minimum_required( VERSION 3.8 )

set(CFLAGS -std=c99)

project( glstarter )

set(CGLM_DIR deps/cglm-0.8.3)

set(CGLM_SOURCES ${CGLM_DIR}/src/euler.c
  ${CGLM_DIR}/src/affine.c ${CGLM_DIR}/src/io.c
  ${CGLM_DIR}/src/quat.c ${CGLM_DIR}/src/cam.c
  ${CGLM_DIR}/src/vec2.c ${CGLM_DIR}/src/vec3.c
  ${CGLM_DIR}/src/vec4.c ${CGLM_DIR}/src/mat2.c
  ${CGLM_DIR}/src/mat3.c ${CGLM_DIR}/src/mat4.c
  ${CGLM_DIR}/src/plane.c ${CGLM_DIR}/src/frustum.c
  ${CGLM_DIR}/src/box.c ${CGLM_DIR}/src/project.c
  ${CGLM_DIR}/src/sphere.c ${CGLM_DIR}/src/ease.c
  ${CGLM_DIR}/src/curve.c ${CGLM_DIR}/src/bezier.c
  ${CGLM_DIR}/src/ray.c ${CGLM_DIR}/src/affine2d.c
  ${CGLM_DIR}/src/clipspace/persp_lh_zo.c ${CGLM_DIR}/src/clipspace/persp_rh_zo.c
  ${CGLM_DIR}/src/clipspace/persp_lh_no.c ${CGLM_DIR}/src/clipspace/persp_rh_no.c
  ${CGLM_DIR}/src/clipspace/ortho_lh_zo.c ${CGLM_DIR}/src/clipspace/ortho_rh_zo.c
  ${CGLM_DIR}/src/clipspace/ortho_lh_no.c ${CGLM_DIR}/src/clipspace/ortho_rh_no.c
  ${CGLM_DIR}/src/clipspace/view_lh_zo.c ${CGLM_DIR}/src/clipspace/view_rh_zo.c
  ${CGLM_DIR}/src/clipspace/view_lh_no.c ${CGLM_DIR}/src/clipspace/view_rh_no.c
  )
  

find_package( OpenGL REQUIRED )

add_executable( glstarter  src/main.c deps/glfw-3.3.4/deps/glad_gl.c ${CGLM_SOURCES})

find_package(GLEW REQUIRED)
if (GLEW_FOUND)
    message("Found GLEW " ${GLEW_LIBRARIES})
    include_directories(${GLEW_INCLUDE_DIRS})
    target_link_libraries(glstarter ${GLEW_LIBRARIES})
endif()

set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)

include_directories( deps/glfw-3.3.4/deps/)
include_directories( ${CGLM_DIR}/include)

add_subdirectory(deps/glfw-3.3.4 EXCLUDE_FROM_ALL)

message(" opengl = " ${OPENGL_opengl_LIBRARY})
target_link_libraries(glstarter  glfw ${OPENGL_opengl_LIBRARY})

 






#target_link_libraries( OpenGL-starter ${OPENGL_LIBRARIES} glfw glm )

#target_include_directories(OpenGL-starter PRIVATE lib/glfw/deps/ include)

#install(TARGETS OpenGL-starter RUNTIME DESTINATION bin)
