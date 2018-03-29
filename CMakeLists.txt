cmake_minimum_required(VERSION 3.1)
project(beam)

enable_testing()

function(add_test_snippet EXE_NAME LIB_NAME)
    add_executable(${EXE_NAME} ${EXE_NAME}.cpp)
    add_dependencies(${EXE_NAME} ${LIB_NAME})
	target_link_libraries(${EXE_NAME} ${LIB_NAME}) 
    add_test( ${EXE_NAME} ${EXE_NAME} )
endfunction()

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall")
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
if(CMAKE_BUILD_TYPE MATCHES "Debug")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O0 -ggdb3")
else()
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3")
endif()

message(${PROJECT_SOURCE_DIR})
include_directories(${PROJECT_SOURCE_DIR})

add_subdirectory(miner)
add_subdirectory(chain)


set_target_properties(miner
    PROPERTIES
    ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
    LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
    RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
)