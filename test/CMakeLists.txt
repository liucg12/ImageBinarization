cmake_minimum_required(VERSION 2.8)

# set runtime directory
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR})

include(gtest.cmake)

find_package(OpenCV REQUIRED)
if(OpenCV_VERSION VERSION_LESS "3.0.0")
  message(FATAL_ERROR "ERROR: Can't find OpenCV 3.0.0+")
endif()

# Generate executable file
add_executable(Test
	${CMAKE_CURRENT_SOURCE_DIR}/NatBinarizationTest.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/NiblackBinarizationTest.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/SauvolaBinarizationTest.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/NickBinarizationTest.cpp)

include_directories(${OpenCV_INCLUDE_DIRS})

# Link libraries
target_link_libraries(Test ImageBinarization gtest gtest_main ${OpenCV_LIBS} ${PYTHON_LIBRARIES})

# Copy Files
file(COPY "${CMAKE_CURRENT_SOURCE_DIR}/images/" DESTINATION ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/images/) 