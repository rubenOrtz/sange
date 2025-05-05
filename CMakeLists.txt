cmake_minimum_required(VERSION 3.10)

project(sange CXX)
set(CMAKE_CXX_STANDARD 17)

if (DEFINED NODE_ADDON_INC)
    include_directories(${NODE_ADDON_INC})
endif()

include_directories(${CMAKE_JS_INC})
include_directories(${NODE_ADDON_INC})

if("${CMAKE_BUILD_TYPE}" STREQUAL "Debug")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DSANGE_DEBUG")
endif()

add_library(sange SHARED
	"src/message.cpp"
	"src/wrapper.cpp"
	"src/player.cpp"
	"src/addon.cpp"
)

target_link_libraries(sange avformat avcodec avutil avfilter uv opus pthread sodium ${CMAKE_JS_LIB})
set_target_properties(sange PROPERTIES PREFIX "" SUFFIX ".node")
