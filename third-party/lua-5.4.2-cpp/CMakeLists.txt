cmake_minimum_required(VERSION 3.11)

project (lua54)

if(LUA_BUILD_AS_DLL)
    add_library(lua54 SHARED)
else()
    add_library(lua54 STATIC)
endif()

if(WIN32)
    add_definitions( -D_CRT_SECURE_NO_WARNINGS )
elseif(CMAKE_SYSTEM_NAME MATCHES "Linux")
    add_definitions( -DLUA_USE_LINUX )
    list(APPEND LINK_LIBRARIES readline dl m)
else()
    add_definitions( -DLUA_USE_MACOSX )
    list(APPEND LINK_LIBRARIES readline)
endif()

if(WIN32)
    if(LUA_BUILD_AS_DLL)
        target_compile_definitions(lua54 PUBLIC -DLUA_BUILD_AS_DLL)
    endif(LUA_BUILD_AS_DLL)
endif(WIN32)

target_sources(lua54 PRIVATE

    #SOURCES
    ${lua54_SOURCE_DIR}/src/lapi.cpp
    ${lua54_SOURCE_DIR}/src/lauxlib.cpp
    ${lua54_SOURCE_DIR}/src/lbaselib.cpp
    ${lua54_SOURCE_DIR}/src/lcode.cpp
    ${lua54_SOURCE_DIR}/src/lcorolib.cpp
    ${lua54_SOURCE_DIR}/src/lctype.cpp
    ${lua54_SOURCE_DIR}/src/ldblib.cpp
    ${lua54_SOURCE_DIR}/src/ldebug.cpp
    ${lua54_SOURCE_DIR}/src/ldo.cpp
    ${lua54_SOURCE_DIR}/src/ldump.cpp
    ${lua54_SOURCE_DIR}/src/lfunc.cpp
    ${lua54_SOURCE_DIR}/src/lgc.cpp
    ${lua54_SOURCE_DIR}/src/linit.cpp
    ${lua54_SOURCE_DIR}/src/liolib.cpp
    ${lua54_SOURCE_DIR}/src/llex.cpp
    ${lua54_SOURCE_DIR}/src/lmathlib.cpp
    ${lua54_SOURCE_DIR}/src/lmem.cpp
    ${lua54_SOURCE_DIR}/src/loadlib.cpp
    ${lua54_SOURCE_DIR}/src/lobject.cpp
    ${lua54_SOURCE_DIR}/src/lopcodes.cpp
    ${lua54_SOURCE_DIR}/src/loslib.cpp
    ${lua54_SOURCE_DIR}/src/lparser.cpp
    ${lua54_SOURCE_DIR}/src/lstate.cpp
    ${lua54_SOURCE_DIR}/src/lstring.cpp
    ${lua54_SOURCE_DIR}/src/lstrlib.cpp
    ${lua54_SOURCE_DIR}/src/ltable.cpp
    ${lua54_SOURCE_DIR}/src/ltablib.cpp
    ${lua54_SOURCE_DIR}/src/ltm.cpp
    ${lua54_SOURCE_DIR}/src/lundump.cpp
    ${lua54_SOURCE_DIR}/src/lutf8lib.cpp
    ${lua54_SOURCE_DIR}/src/lvm.cpp
    ${lua54_SOURCE_DIR}/src/lzio.cpp
)

