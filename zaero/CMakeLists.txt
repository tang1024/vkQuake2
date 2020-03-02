project(zaero C)

################################################################################
# Source groups
################################################################################
set(Header_Files
    "g_local.h"
    "game.h"
    "m_actor.h"
    "m_berserk.h"
    "m_boss2.h"
    "m_boss31.h"
    "m_boss32.h"
    "m_brain.h"
    "m_chick.h"
    "m_flipper.h"
    "m_float.h"
    "m_flyer.h"
    "m_gladiator.h"
    "m_gunner.h"
    "m_hover.h"
    "m_infantry.h"
    "m_insane.h"
    "m_medic.h"
    "m_mutant.h"
    "m_parasite.h"
    "m_player.h"
    "m_rider.h"
    "m_soldier.h"
    "m_supertank.h"
    "m_tank.h"
    "q_shared.h"
    "z_anim.h"
    "z_boss.h"
    "z_debug.h"
    "z_frames.h"
    "z_handler.h"
    "z_hound.h"
    "z_list.h"
    "z_menu.h"
    "z_sentien.h"
)
source_group("Header Files" FILES ${Header_Files})

set(Source_Files
    "g_ai.c"
    "g_cmds.c"
    "g_combat.c"
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
    "g_turret.c"
    "g_utils.c"
    "g_weapon.c"
    "m_actor.c"
    "m_berserk.c"
    "m_boss2.c"
    "m_boss3.c"
    "m_boss31.c"
    "m_boss32.c"
    "m_brain.c"
    "m_chick.c"
    "m_flash.c"
    "m_flipper.c"
    "m_float.c"
    "m_flyer.c"
    "m_gladiator.c"
    "m_gunner.c"
    "m_hover.c"
    "m_infantry.c"
    "m_insane.c"
    "m_medic.c"
    "m_move.c"
    "m_mutant.c"
    "m_parasite.c"
    "m_soldier.c"
    "m_supertank.c"
    "m_tank.c"
    "p_client.c"
    "p_hud.c"
    "p_trail.c"
    "p_view.c"
    "p_weapon.c"
    "q_shared.c"
    "z_acannon.c"
    "z_ai.c"
    "z_anim.c"
    "z_boss.c"
    "z_camera.c"
    "z_debug.c"
    "z_frames.c"
    "z_handler.c"
    "z_hound.c"
    "z_item.c"
    "z_list.c"
    "z_mtest.c"
    "z_sentien.c"
    "z_spawn.c"
    "z_trigger.c"
    "z_weapon.c"
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
        OUTPUT_DIRECTORY_DEBUG   "${CMAKE_SOURCE_DIR}/Quake2/zaero"
        OUTPUT_DIRECTORY_RELEASE "${CMAKE_SOURCE_DIR}/Quake2/zaero"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        OUTPUT_DIRECTORY_DEBUG   "${CMAKE_SOURCE_DIR}/Quake2/zaero"
        OUTPUT_DIRECTORY_RELEASE "${CMAKE_SOURCE_DIR}/Quake2/zaero"
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
        INTERPROCEDURAL_OPTIMIZATION_DEBUG   "FALSE"
        INTERPROCEDURAL_OPTIMIZATION_RELEASE "TRUE"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    set_target_properties(${PROJECT_NAME} PROPERTIES
        INTERPROCEDURAL_OPTIMIZATION_DEBUG   "FALSE"
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
        "_WINDOWS"
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
                /JMC;
                /Od;
                /RTC1;
                /MDd;
                /ZI
            >
            $<$<CONFIG:Release>:
                /O2;
                /Oi;
                /GF;
                /MD;
                /Gy;
                ${DEFAULT_CXX_DEBUG_INFORMATION_FORMAT}
            >
            /W3;
            /wd4996;
            ${DEFAULT_CXX_EXCEPTION_HANDLING}
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
        target_compile_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                /JMC;
                /Gm-;
                /Od;
                /RTC1;
                /MDd;
                /ZI
            >
            $<$<CONFIG:Release>:
                /O2;
                /Oi;
                /GF;
                /MD;
                /Gy;
                ${DEFAULT_CXX_DEBUG_INFORMATION_FORMAT}
            >
            /W3;
            /wd4996;
            ${DEFAULT_CXX_EXCEPTION_HANDLING}
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

