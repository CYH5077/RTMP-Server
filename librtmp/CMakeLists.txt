cmake_minimum_required(VERSION 3.6)

project(rtmp)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if(WIN32 AND MSVC)
    set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS TRUE)
elseif(LINUX)
    set(CMAKE_CXX_FLAGS -Wall)
	set(CMAKE_CXX_FLAGS_RELEASE "-O3")
	set(CMAKE_CXX_FLAGS_DEBUG "-g")
endif()

set(LIB_RTMP_INSTALL_DIR ${CMAKE_CURRENT_SOURCE_DIR}/build/${PROJECT_NAME})
set(LIB_RTMP_INCLUDE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/include)

add_library(${PROJECT_NAME})

find_package(boost_asio CONFIG REQUIRED)
target_link_libraries(${PROJECT_NAME} PUBLIC Boost::asio)
target_include_directories(${PROJECT_NAME} PUBLIC ${LIB_RTMP_INCLUDE_DIR})

add_subdirectory(src)
#add_subdirectory(test)