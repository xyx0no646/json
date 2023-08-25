
cmake_minimum_required(VERSION 3.12)
project(json_krkrsdl2)

include(FetchContent)

FetchContent_Declare(
	krkrsdl2-tp_stub
	URL https://github.com/krkrsdl2/krkrsdl2/releases/download/latest/krkrsdl2-tp_stub.tar.gz
)

FetchContent_MakeAvailable(krkrsdl2-tp_stub)

set(JSON_SRC_DIR ${CMAKE_CURRENT_SOURCE_DIR})
file(STRINGS ${JSON_SRC_DIR}/src_list/sources.txt JSON_SRC)
file(STRINGS ${JSON_SRC_DIR}/src_list/includes.txt JSON_INCLUDES)
list(TRANSFORM JSON_SRC PREPEND ${JSON_SRC_DIR}/)
list(TRANSFORM JSON_INCLUDES PREPEND ${JSON_SRC_DIR}/)

add_library(json MODULE)
set_target_properties(json PROPERTIES CXX_STANDARD 11)
set_target_properties(json PROPERTIES PREFIX "")
target_sources(json PRIVATE ${JSON_SRC})
target_include_directories(json PRIVATE ${JSON_INCLUDES})
target_link_libraries(json tp_stub)
