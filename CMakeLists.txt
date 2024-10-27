cmake_minimum_required(VERSION 3.0.0)
project(vulkan-test)

set(CMAKE_CXX_STANDARD 20)

find_package(Vulkan REQUIRED)

file(GLOB_RECURSE SOURCES src/*.cpp)
file(GLOB_RECURSE EXTERNAL_SOURCES external/src/*.cpp external/src/*.c)

add_executable(vulkan-test ${SOURCES} ${EXTERNAL_SOURCES})
target_include_directories(vulkan-test PRIVATE external/include)
if(WIN32)
	target_link_directories(vulkan-test PRIVATE external/lib/GLFW)
	target_link_libraries(vulkan-test PRIVATE libglfw3.a)
elseif(UNIX)
	target_link_libraries(vulkan-test PRIVATE glfw)
endif()

target_include_directories(vulkan-test PRIVATE ${Vulkan_INCLUDE_DIRS})
target_link_libraries(vulkan-test PRIVATE ${Vulkan_LIBRARIES})
