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
endif ()

set(JSON_BuildTests OFF CACHE INTERNAL "")
add_subdirectory(json)
