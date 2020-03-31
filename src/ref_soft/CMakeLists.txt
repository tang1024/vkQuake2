project(ref_soft C)

################################################################################
# Source groups
################################################################################
set(Header_Files
    "../client/ref.h"
    "../game/q_shared.h"
    "../qcommon/qcommon.h"
    "../qcommon/qfiles.h"
    "../win32/rw_win.h"
    "../win32/winquake.h"
    "adivtab.h"
    "anorms.h"
    "r_dither.h"
    "r_local.h"
    "r_model.h"
    "rand1k.h"
)
source_group("Header Files" FILES ${Header_Files})

set(Source_Files
    "../game/q_shared.c"
    "../win32/q_shwin.c"
    "../win32/rw_ddraw.c"
    "../win32/rw_dib.c"
    "../win32/rw_imp.c"
    "r_aclip.c"
    "r_alias.c"
    "r_bsp.c"
    "r_draw.c"
    "r_edge.c"
    "r_image.c"
    "r_light.c"
    "r_main.c"
    "r_misc.c"
    "r_model.c"
    "r_part.c"
    "r_poly.c"
    "r_polyse.c"
    "r_rast.c"
    "r_scan.c"
    "r_sprite.c"
    "r_surf.c"
)
source_group("Source Files" FILES ${Source_Files})

set(ALL_FILES
    ${Header_Files}
    ${Source_Files}
)

################################################################################
# Target
################################################################################
add_library(${PROJECT_NAME} SHARED ${ALL_FILES})

use_props(${PROJECT_NAME} "${CMAKE_CONFIGURATION_TYPES}" "${DEFAULT_CXX_PROPS}")
################################################################################
# Output directory
################################################################################
if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        OUTPUT_DIRECTORY_DEBUG   "${CMAKE_SOURCE_DIR}/Quake2/"
        OUTPUT_DIRECTORY_RELEASE "${CMAKE_SOURCE_DIR}/Quake2/"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        OUTPUT_DIRECTORY_DEBUG   "${CMAKE_SOURCE_DIR}/Quake2/"
        OUTPUT_DIRECTORY_RELEASE "${CMAKE_SOURCE_DIR}/Quake2/"
    )
endif()
if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        INTERPROCEDURAL_OPTIMIZATION_RELEASE "TRUE"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        INTERPROCEDURAL_OPTIMIZATION_RELEASE "TRUE"
    )
endif()
################################################################################
# Compile definitions
################################################################################
if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    target_compile_definitions(${PROJECT_NAME} PRIVATE
        "$<$<CONFIG:Release>:"
            "NDEBUG"
        ">"
        "_CRT_SECURE_NO_DEPRECATE;"
        "_CRT_SECURE_NO_WARNINGS;"
        "WIN32;"
        "_WINDOWS"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    target_compile_definitions(${PROJECT_NAME} PRIVATE
        "$<$<CONFIG:Release>:"
            "NDEBUG"
        ">"
        "_CRT_SECURE_NO_DEPRECATE;"
        "_CRT_SECURE_NO_WARNINGS;"
        "WIN32;"
        "_WINDOWS"
    )
endif()

################################################################################
# Compile and link options
################################################################################
if(MSVC)
    if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
        target_compile_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                /Gm-;
                /Od;
                /MDd;
                /Zi
            >
            $<$<CONFIG:Release>:
                /O2;
                /GF;
                /MD;
                /Gy;
                ${DEFAULT_CXX_DEBUG_INFORMATION_FORMAT}
            >
            /W3;
            /wd4312;
            /wd4996;
            ${DEFAULT_CXX_EXCEPTION_HANDLING};
            /Y-
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
        target_compile_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                /Gm-;
                /Od;
                /MDd;
                /ZI
            >
            $<$<CONFIG:Release>:
                /O2;
                /GF;
                /MD;
                /Gy;
                ${DEFAULT_CXX_DEBUG_INFORMATION_FORMAT}
            >
            /W3;
            /wd4996;
            ${DEFAULT_CXX_EXCEPTION_HANDLING};
            /Y-
        )
    endif()
    if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
        target_link_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                /NODEFAULTLIB:libc;
                /DEBUG;
                /INCREMENTAL
            >
            $<$<CONFIG:Release>:
                /INCREMENTAL:NO
            >
            /NOLOGO;
            /SUBSYSTEM:WINDOWS
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
        target_link_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                /NODEFAULTLIB:libc;
                /DEBUG;
                /INCREMENTAL
            >
            $<$<CONFIG:Release>:
                /INCREMENTAL:NO
            >
            /NOLOGO;
            /SUBSYSTEM:WINDOWS
        )
    endif()
endif()

################################################################################
# Dependencies
################################################################################
if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    set(ADDITIONAL_LIBRARY_DEPENDENCIES
        "winmm"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    set(ADDITIONAL_LIBRARY_DEPENDENCIES
        "winmm"
    )
endif()
target_link_libraries(${PROJECT_NAME} PUBLIC "${ADDITIONAL_LIBRARY_DEPENDENCIES}")

