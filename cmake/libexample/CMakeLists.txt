cmake_minimum_required(VERSION 3.20)
project(libexample)

include_directories(${CMAKE_CURRENT_SOURCE_DIR})

add_executable(myprog
	myprog.cpp)
target_link_libraries(myprog
		mylib)

# add_library(TARGET [STATIC  | SHARED | MODULE ] sources...)
add_library(mylib
		mylib.h
		mylib.cpp)
