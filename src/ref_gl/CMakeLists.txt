set(ROOT_NAMESPACE ref_gl)

################################################################################
# Source groups
################################################################################
set(Header_Files
    "../client/qmenu.h"
    "../client/ref.h"
    "../game/q_shared.h"
    "../qcommon/qcommon.h"
    "../qcommon/qfiles.h"
    "anorms.h"
    "anormtab.h"
    "gl_local.h"
    "gl_model.h"
    "qgl.h"
    "warpsin.h"
)
source_group("Header Files" FILES ${Header_Files})

set(Resource_Files
    "ref_gl.def"
)
source_group("Resource Files" FILES ${Resource_Files})

set(Source_Files
    "../game/q_shared.c"
    "../win32/glw_imp.c"
    "../win32/q_shwin.c"
    "../win32/qgl_win.c"
    "gl_draw.c"
    "gl_image.c"
    "gl_light.c"
    "gl_mesh.c"
    "gl_model.c"
    "gl_rmain.c"
    "gl_rmisc.c"
    "gl_rsurf.c"
    "gl_warp.c"
)
source_group("Source Files" FILES ${Source_Files})

set(ALL_FILES
    ${Header_Files}
    ${Resource_Files}
    ${Source_Files}
)

################################################################################
# Target
################################################################################
add_library(${ROOT_NAMESPACE} SHARED ${ALL_FILES})

################################################################################
# Output directory
################################################################################
if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    set_target_properties(${ROOT_NAMESPACE} PROPERTIES
        OUTPUT_DIRECTORY_DEBUG   "${CMAKE_SOURCE_DIR}/Quake2/"
        OUTPUT_DIRECTORY_RELEASE "${CMAKE_SOURCE_DIR}/Quake2/"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    set_target_properties(${ROOT_NAMESPACE} PROPERTIES
        OUTPUT_DIRECTORY_DEBUG   "${CMAKE_SOURCE_DIR}/Quake2/"
        OUTPUT_DIRECTORY_RELEASE "${CMAKE_SOURCE_DIR}/Quake2/"
    )
endif()
################################################################################
# Compile definitions
################################################################################
if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    target_compile_definitions(${ROOT_NAMESPACE} PRIVATE
                                "_DEBUG"
                                "NDEBUG"
                                "_CRT_SECURE_NO_DEPRECATE;"
                                "_CRT_SECURE_NO_WARNINGS;"
                                "WIN32;"
                                "_WINDOWS;"
                                "_USRDLL;"
                                "REF_GL_EXPORTS"
                               )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    target_compile_definitions(${ROOT_NAMESPACE} PRIVATE
                               "_DEBUG"
                               "NDEBUG"
                               "_CRT_SECURE_NO_DEPRECATE;"
                               "_CRT_SECURE_NO_WARNINGS;"
                               "WIN32;"
                               "_WINDOWS;"
                               "_USRDLL;"
                               "REF_GL_EXPORTS"
                               )
endif()

################################################################################
# Dependencies
################################################################################
if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    set(ADDITIONAL_LIBRARY_DEPENDENCIES
        "opengl32;"
        "winmm"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    set(ADDITIONAL_LIBRARY_DEPENDENCIES
        "opengl32;"
        "winmm"
    )
endif()
target_link_libraries(${ROOT_NAMESPACE} PUBLIC "${ADDITIONAL_LIBRARY_DEPENDENCIES}")

