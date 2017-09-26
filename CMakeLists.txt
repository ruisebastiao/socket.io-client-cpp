cmake_minimum_required(VERSION 3.1.0 FATAL_ERROR)

project(sioclient)

# Find source files
file(GLOB SOURCES src/*.cpp)

# Include header files
include_directories(src/*.h)

# Create shared library
add_library(${PROJECT_NAME} SHARED ${SOURCES})

# Install library
install(TARGETS ${PROJECT_NAME} DESTINATION lib/)

# Install library headers
file(GLOB HEADERS src/*.h)
install(FILES ${HEADERS} DESTINATION include/)
