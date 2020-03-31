project(ctf C)

################################################################################
# Source groups
################################################################################
set(Header_Files
    "g_ctf.h"
    "g_local.h"
    "game.h"
    "m_player.h"
    "p_menu.h"
    "q_shared.h"
)
source_group("Header Files" FILES ${Header_Files})

set(Source_Files
    "g_ai.c"
    "g_chase.c"
    "g_cmds.c"
    "g_combat.c"
    "g_ctf.c"
    "g_func.c"
    "g_items.c"
    "g_main.c"
    "g_misc.c"
    "g_monster.c"
    "g_phys.c"
    "g_save.c"
    "g_spawn.c"
    "g_svcmds.c"
    "g_target.c"
    "g_trigger.c"
    "g_utils.c"
    "g_weapon.c"
    "m_move.c"
    "p_client.c"
    "p_hud.c"
    "p_menu.c"
    "p_trail.c"
    "p_view.c"
    "p_weapon.c"
    "q_shared.c"
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
# Target name
################################################################################
if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        TARGET_NAME_DEBUG   "gamex64$ENV{TargetExt}"
        TARGET_NAME_RELEASE "gamex64$ENV{TargetExt}"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        TARGET_NAME_DEBUG   "gamex86$ENV{TargetExt}"
        TARGET_NAME_RELEASE "gamex86$ENV{TargetExt}"
    )
endif()
################################################################################
# Output directory
################################################################################
if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        OUTPUT_DIRECTORY_DEBUG   "${CMAKE_SOURCE_DIR}/Quake2/ctf"
        OUTPUT_DIRECTORY_RELEASE "${CMAKE_SOURCE_DIR}/Quake2/ctf"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        OUTPUT_DIRECTORY_DEBUG   "${CMAKE_SOURCE_DIR}/Quake2/ctf"
        OUTPUT_DIRECTORY_RELEASE "${CMAKE_SOURCE_DIR}/Quake2/ctf"
    )
endif()
if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        ARCHIVE_OUTPUT_DIRECTORY_DEBUG   "${OUTPUT_DIRECTORY}"
        ARCHIVE_OUTPUT_DIRECTORY_RELEASE "${OUTPUT_DIRECTORY}"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        ARCHIVE_OUTPUT_DIRECTORY_DEBUG   "${OUTPUT_DIRECTORY}"
        ARCHIVE_OUTPUT_DIRECTORY_RELEASE "${OUTPUT_DIRECTORY}"
    )
endif()
if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        ARCHIVE_OUTPUT_NAME_DEBUG   "${TARGET_NAME}"
        ARCHIVE_OUTPUT_NAME_RELEASE "${TARGET_NAME}"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        ARCHIVE_OUTPUT_NAME_DEBUG   "${TARGET_NAME}"
        ARCHIVE_OUTPUT_NAME_RELEASE "${TARGET_NAME}"
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
        "$<$<CONFIG:Debug>:"
            "_DEBUG"
        ">"
        "$<$<CONFIG:Release>:"
            "NDEBUG"
        ">"
        "_CRT_SECURE_NO_DEPRECATE;"
        "_CRT_SECURE_NO_WARNINGS;"
        "WIN32;"
        "_WINDOWS;"
        "_USRDLL"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    target_compile_definitions(${PROJECT_NAME} PRIVATE
        "$<$<CONFIG:Debug>:"
            "_DEBUG"
        ">"
        "$<$<CONFIG:Release>:"
            "NDEBUG"
        ">"
        "_CRT_SECURE_NO_DEPRECATE;"
        "_CRT_SECURE_NO_WARNINGS;"
        "WIN32;"
        "_WINDOWS;"
        "_USRDLL"
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
                /Oi;
                /MD;
                /Gy;
                ${DEFAULT_CXX_DEBUG_INFORMATION_FORMAT}
            >
            /W3;
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
                /Oi;
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
                /DEBUG;
                /INCREMENTAL
            >
            $<$<CONFIG:Release>:
                /OPT:REF;
                /OPT:ICF;
                /INCREMENTAL:NO
            >
            /NOLOGO;
            /SUBSYSTEM:WINDOWS
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
        target_link_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                /DEBUG;
                /INCREMENTAL
            >
            $<$<CONFIG:Release>:
                /OPT:REF;
                /OPT:ICF;
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

