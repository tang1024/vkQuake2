cmake_minimum_required(VERSION 3.13.0 FATAL_ERROR)

project(quake2 C)

################################################################################
# Set target arch type if empty. Visual studio solution generator provides it.
################################################################################
if(NOT CMAKE_VS_PLATFORM_NAME)
    set(CMAKE_VS_PLATFORM_NAME "x64")
endif()
message("${CMAKE_VS_PLATFORM_NAME} architecture in use")

if(NOT ("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64"
     OR "${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86"))
    message(FATAL_ERROR "${CMAKE_VS_PLATFORM_NAME} arch is not supported!")
endif()

################################################################################
# Global configuration types
################################################################################
set(CMAKE_CONFIGURATION_TYPES
    "Debug"
    "Release"
    CACHE STRING "" FORCE
)

################################################################################
# Sub-projects
################################################################################
add_subdirectory(game)
#add_subdirectory(ref_soft)
add_subdirectory(ref_gl)
#add_subdirectory(ref_vk)
#add_subdirectory(ctf)
#add_subdirectory(rogue)
#add_subdirectory(xatrix)
#add_subdirectory(zaero)

set(ROOT_NAMESPACE quake2)

################################################################################
# Source groups
################################################################################
set(Header_Files
    "client/anorms.h"
    "client/cdaudio.h"
    "client/client.h"
    "client/console.h"
    "client/input.h"
    "client/keys.h"
    "client/miniaudio.h"
    "client/qmenu.h"
    "client/ref.h"
    "client/screen.h"
    "client/snd_loc.h"
    "client/snd_miniaudio.h"
    "client/sound.h"
    "client/vid.h"
    "game/game.h"
    "game/q_shared.h"
    "qcommon/qcommon.h"
    "qcommon/qfiles.h"
    "server/server.h"
    "win32/conproc.h"
    "win32/winquake.h"
)
source_group("Header Files" FILES ${Header_Files})

set(Source_Files
    "client/cl_cin.c"
    "client/cl_ents.c"
    "client/cl_fx.c"
    "client/cl_input.c"
    "client/cl_inv.c"
    "client/cl_main.c"
    "client/cl_newfx.c"
    "client/cl_parse.c"
    "client/cl_pred.c"
    "client/cl_scrn.c"
    "client/cl_tent.c"
    "client/cl_view.c"
    "client/console.c"
    "client/keys.c"
    "client/menu.c"
    "client/qmenu.c"
    "client/snd_dma.c"
    "client/snd_mem.c"
    "client/snd_miniaudio.c"
    "client/snd_mix.c"
    "client/x86.c"
    "game/m_flash.c"
    "game/q_shared.c"
    "qcommon/cmd.c"
    "qcommon/cmodel.c"
    "qcommon/common.c"
    "qcommon/crc.c"
    "qcommon/cvar.c"
    "qcommon/files.c"
    "qcommon/md4.c"
    "qcommon/net_chan.c"
    "qcommon/pmove.c"
    "server/sv_ccmds.c"
    "server/sv_ents.c"
    "server/sv_game.c"
    "server/sv_init.c"
    "server/sv_main.c"
    "server/sv_send.c"
    "server/sv_user.c"
    "server/sv_world.c"
    "win32/cd_win.c"
    "win32/conproc.c"
    "win32/in_win.c"
    "win32/net_wins.c"
    "win32/q_shwin.c"
    "win32/snd_win.c"
    "win32/sys_win.c"
    "win32/vid_dll.c"
    "win32/vid_menu.c"
)
source_group("Source Files" FILES ${Source_Files})

set(ALL_FILES
    ${Header_Files}
    ${Source_Files}
)

################################################################################
# Target
################################################################################
add_executable(${ROOT_NAMESPACE} ${ALL_FILES})

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

################################################################################
# Compile definitions
################################################################################
if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    target_compile_definitions(${ROOT_NAMESPACE} PRIVATE
    "_DEBUG"
    "WIN_DEBUG_CONSOLE"
    "NDEBUG"
    "_CRT_SECURE_NO_DEPRECATE"
    "_CRT_SECURE_NO_WARNINGS"
    "WIN32"
    "_WINDOWS"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    target_compile_definitions(${ROOT_NAMESPACE} PRIVATE
    "_DEBUG"
    "WIN_DEBUG_CONSOLE"
    "NDEBUG"
    "_CRT_SECURE_NO_DEPRECATE"
    "_CRT_SECURE_NO_WARNINGS"
    "WIN32"
    "_WINDOWS"
    )
endif()


################################################################################
# Dependencies
################################################################################
add_dependencies(${ROOT_NAMESPACE}
    #ref_soft
    ref_gl
    #ref_vk
    game
)

if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    set(ADDITIONAL_LIBRARY_DEPENDENCIES
        "winmm;"
        "wsock32"
        )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    set(ADDITIONAL_LIBRARY_DEPENDENCIES
        "winmm;"
        "wsock32"
        )
endif()
target_link_libraries(${ROOT_NAMESPACE} PUBLIC "${ADDITIONAL_LIBRARY_DEPENDENCIES}")
