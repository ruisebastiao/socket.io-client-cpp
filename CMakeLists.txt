cmake_minimum_required(VERSION 3.1.0 FATAL_ERROR)

project(sioclient)


aux_source_directory(src/ ALL_SRC)
aux_source_directory(src/internal ALL_SRC)


# Include header files
include_directories(src/*.h)

set(BOOST_VER "1.55.0" CACHE STRING "boost version" )

set(Boost_USE_MULTITHREADED ON) 
set(Boost_USE_STATIC_RUNTIME OFF) 
find_package(Boost ${BOOST_VER} REQUIRED COMPONENTS system date_time random) 


# Create shared library
add_library(${PROJECT_NAME} SHARED ${SOURCES})

set_property(TARGET sioclient PROPERTY CXX_STANDARD 11)
set_property(TARGET sioclient PROPERTY CXX_STANDARD_REQUIRED ON)
target_link_libraries(sioclient PRIVATE ${Boost_LIBRARIES})

# Install library
install(TARGETS ${PROJECT_NAME} DESTINATION lib/)

# Install library headers
file(GLOB HEADERS src/*.h)
install(FILES ${HEADERS} DESTINATION include/)
