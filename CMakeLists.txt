# Minimum requirement.
cmake_minimum_required(VERSION 3.10)

# Project name.
project(WidTools)

# Build options.
option(CONFIG_BUILD_WIDBSP "Build the BSP tool" ON)
option(CONFIG_BUILD_WIDVIS "Build the VIS tool" ON)
option(CONFIG_BUILD_WIDRAD "Build the RAD tool" ON)
option(CONFIG_BUILD_WIDDATA "Build the data utility tool" ON)

###############################################################################
# COMMON SOURCES & HEADERS
###############################################################################
SET(SRC_COMMON
    common/bspfile.c
    common/cmdlib.c
    common/l3dslib.c 
    common/lbmlib.c
    common/llwolib.c 
    common/mathlib.c 
    common/mdfour.c 
    common/polylib.c 
    common/scriplib.c 
    common/threads.c 
    common/trilib.c
)
SET(HEADERS_COMMON
    common/bspfile.h
    common/cmdlib.h
    common/flipper.h
    common/l3dslib.h 
    common/lbmlib.h
    common/llwolib.h
    common/mathlib.h 
    common/mdfour.h
    common/polylib.h
    common/qfiles.h
    common/scriplib.h 
    common/threads.h 
    common/trilib.h
)


###############################################################################
# WIDBSP SOURCES & HEADERS
###############################################################################
SET(SRC_WIDBSP
    widbsp/brushbsp.c
    widbsp/csg.c 
    widbsp/faces.c 
    widbsp/gldraw.c 
    widbsp/leakfile.c 
    widbsp/main.c 
    widbsp/map.c 
    widbsp/portals.c 
    widbsp/prtfile.c 
    widbsp/textures.c 
    widbsp/tree.c 
    widbsp/writebsp.c
)

SET(HEADERS_WIDBSP
    widbsp/qbsp.h
)


###############################################################################
# WIDVIS SOURCES & HEADERS
###############################################################################
SET(SRC_WIDVIS
    widvis/flow.c 
    widvis/main.c 
    widvis/vis.h 
)

SET(HEADERS_WIDVIS
    widvis/vis.h
)


###############################################################################
# WIDRAD SOURCES & HEADERS
###############################################################################
SET(SRC_WIDRAD
    widrad/lightmap.c 
    widrad/main.c 
    widrad/patches.c 
    widrad/trace.c 
)
SET(HEADERS_WIDRAD
    widrad/qrad.h
)


###############################################################################
# WIDATA SOURCES & HEADERS
###############################################################################
SET(SRC_WIDDATA
    widdata/images.c 
    widdata/models.c 
    widdata/sprites.c 
    widdata/tables.c 
    widdata/video.c 
    widdata/main.c
)

SET(HEADERS_WIDDATA
    widdata/anorms.h
    widdata/widdata.h
)

###############################################################################
# PROJECT SETUPS
###############################################################################
###
### WIDBSP
###
if (CONFIG_BUILD_WIDBSP)
    # Create WIDBSP executable.
    add_executable(widbsp
        ${SRC_COMMON}
        ${HEADERS_COMMON}

        ${SRC_WIDBSP}
        ${HEADERS_WIDBSP}
    )
    
    # Add the common dir as include directory.
    include_directories(widbsp PRIVATE common/)
endif()

###
### WIDVIS
###
if (CONFIG_BUILD_WIDVIS)
    # Create WIDBSP executable.
    add_executable(widvis
        ${SRC_COMMON}
        ${HEADERS_COMMON}

        ${SRC_WIDVIS}
        ${HEADERS_WIDVIS}
    )

    # Add the common dir as include directory.
    target_include_directories(widvis PRIVATE common/)
endif()

###
### WIDRAD
###
if (CONFIG_BUILD_WIDRAD)
    # Create WIDBSP executable.
    add_executable(widrad
        ${SRC_COMMON}
        ${HEADERS_COMMON}

        ${SRC_WIDRAD}
        ${HEADERS_WIDRAD}
    )

        # Add the common dir as include directory.
        target_include_directories(widrad PRIVATE common/)
endif()

###
### WIDDATA
###
if (CONFIG_BUILD_WIDDATA)
    # Find the OpenGL Package.
    find_package(OpenGL REQUIRED)
    include_directories( ${OPENGL_INCLUDE_DIRS} )

    # Create WIDBSP executable.
    add_executable(widdata
        ${SRC_COMMON}
        ${HEADERS_COMMON}

        ${SRC_WIDDATA}
        ${HEADERS_WIDDATA}
    )

    # Add the common dir as include directory.
    target_include_directories(widdata PRIVATE common/)
    target_link_libraries(widdata opengl32)
endif()