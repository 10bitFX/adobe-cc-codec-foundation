add_subdirectory(adobe)

# Check if OVERRIDE_FFMPEG is NOT set
if(NOT DEFINED OVERRIDE_FFMPEG)
    message(STATUS "[foundation/external] Using bundled ffmpeg")
    add_subdirectory(ffmpeg)
else()
    message(STATUS "[foundation/external] Using local ffmpeg (OVERRIDE_FFMPEG is set)")
endif()

set( gtest_force_shared_crt ON CACHE BOOL "Always use msvcrt.dll" FORCE)
add_subdirectory(googletest)

if (WIN32)
    add_subdirectory(StackWalker)

    # Construct StackWalkerSdk from StackWalker so that it can be dynamically used in generated projects
    add_library(StackWalkerSdk INTERFACE)
    target_link_libraries(StackWalkerSdk INTERFACE StackWalker)
    target_sources(StackWalkerSdk
        INTERFACE
            ${CMAKE_CURRENT_LIST_DIR}/StackWalker/Main/StackWalker/StackWalker.h
    )
    target_include_directories(StackWalkerSdk 
        INTERFACE
            $<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}/StackWalker/Main/StackWalker>
    )
    
endif ()

set(JSON_BuildTests OFF CACHE INTERNAL "")
add_subdirectory(json)
