cmake_minimum_required (VERSION 3.0.0)
project (main CXX)

SET(CMAKE_EXPORT_COMPILE_COMMANDS 1)
# SET(CMAKE_CXX_COMPILER "g++")

set(CMAKE_CXX_STANDARD 20)

SET(CMAKE_CXX_STANDARD_INCLUDE_DIRECTORIES  ${CMAKE_CXX_IMPLICIT_INCLUDE_DIRECTORIES})


add_subdirectory(googletest-release-1.11.0)


include_directories(include)
file(GLOB SRC src/*.cpp)
add_executable(main ${SRC})
target_link_libraries(main
		PUBLIC
		gtest
		gmock
		gmock_main
		atomic
		)


add_custom_target(
	copy-compile-commands ALL
	${CMAKE_COMMAND} -E copy_if_different
	${CMAKE_BINARY_DIR}/compile_commands.json
	${CMAKE_CURRENT_LIST_DIR}
)
