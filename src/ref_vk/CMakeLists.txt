project(ref_vk C CXX)

################################################################################
# Source groups
################################################################################
set(Header_Files
    "../client/qmenu.h"
    "../client/ref.h"
    "../game/q_shared.h"
    "../qcommon/qcommon.h"
    "../qcommon/qfiles.h"
    "../win32/vk_win.h"
    "anorms.h"
    "anormtab.h"
    "qvk.h"
    "vk_local.h"
    "vk_model.h"
    "vk_shaders.h"
)
source_group("Header Files" FILES ${Header_Files})

set(Resource_Files
    "ref_vk.def"
)
source_group("Resource Files" FILES ${Resource_Files})

set(Source_Files
    "../game/q_shared.c"
    "../win32/q_shwin.c"
    "../win32/vk_imp.c"
    "vk_buffer.c"
    "vk_cmd.c"
    "vk_common.c"
    "vk_device.c"
    "vk_draw.c"
    "vk_image.c"
    "vk_light.c"
    "vk_mem_alloc.cpp"
    "vk_mesh.c"
    "vk_model.c"
    "vk_pipeline.c"
    "vk_rmain.c"
    "vk_rmisc.c"
    "vk_rsurf.c"
    "vk_shaders.c"
    "vk_swapchain.c"
    "vk_validation.c"
    "vk_warp.c"
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
add_library(${PROJECT_NAME} SHARED ${ALL_FILES})

use_props(${PROJECT_NAME} "${CMAKE_CONFIGURATION_TYPES}" "${DEFAULT_CXX_PROPS}")
set(ROOT_NAMESPACE ref_vk)

set_target_properties(${PROJECT_NAME} PROPERTIES
    VS_GLOBAL_KEYWORD "Win32Proj"
)
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
# Include directories
################################################################################
if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    target_include_directories(${PROJECT_NAME} PUBLIC
        "$ENV{VULKAN_SDK}/Include"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    target_include_directories(${PROJECT_NAME} PUBLIC
        "$ENV{VULKAN_SDK}/Include"
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
                /Od;
                ${DEFAULT_CXX_DEBUG_RUNTIME_LIBRARY}
            >
            $<$<CONFIG:Release>:
                /O2;
                /Oi;
                ${DEFAULT_CXX_RUNTIME_LIBRARY};
                /Gy
            >
            /W3;
            ${DEFAULT_CXX_DEBUG_INFORMATION_FORMAT};
            /wd4996;
            ${DEFAULT_CXX_EXCEPTION_HANDLING};
            /Y-
        )
    elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
        target_compile_options(${PROJECT_NAME} PRIVATE
            $<$<CONFIG:Debug>:
                /Od;
                ${DEFAULT_CXX_DEBUG_RUNTIME_LIBRARY}
            >
            $<$<CONFIG:Release>:
                /O2;
                /Oi;
                ${DEFAULT_CXX_RUNTIME_LIBRARY};
                /Gy
            >
            /W3;
            ${DEFAULT_CXX_DEBUG_INFORMATION_FORMAT};
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
            /SUBSYSTEM:WINDOWS
        )
    endif()
endif()

################################################################################
# Dependencies
################################################################################
if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    set(ADDITIONAL_LIBRARY_DEPENDENCIES
        "vulkan-1;"
        "winmm"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    set(ADDITIONAL_LIBRARY_DEPENDENCIES
        "vulkan-1;"
        "winmm"
    )
endif()
target_link_libraries(${PROJECT_NAME} PUBLIC "${ADDITIONAL_LIBRARY_DEPENDENCIES}")

if("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x64")
    target_link_directories(${PROJECT_NAME} PUBLIC
        "$ENV{VULKAN_SDK}/Lib"
    )
elseif("${CMAKE_VS_PLATFORM_NAME}" STREQUAL "x86")
    target_link_directories(${PROJECT_NAME} PUBLIC
        "$ENV{VULKAN_SDK}/Lib32"
    )
endif()

