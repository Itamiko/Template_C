cmake_minimum_required(VERSION 3.17.0)
project(template_c C)

set(srouces
	src/main.c
)

add_executable(${CMAKE_PROJECT_NAME} ${SOURCES})

if(CMAKE_BUILD_TYPE MATCHES Release)
	set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -s")
elseif(CMAKE_BUILD_TYPE MATCHES Debug)
	set(default_build_type "Debug")
endif()

if(NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
	message(STATUS "Setting build type to '${DEFAULT_CMAKE_BUILD_TYPE}' as none was specified.")
	set(CMAKE_BUILD_TYPE ${DEFAULT_CMAKE_BUILD_TYPE}
		CACHE STRING "Choose the type of build." FORCE)
	set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS Debug Release MinSizeRel RelWithDebInfo)
endif()

target_include_directories(${CMAKE_PROJECT_NAME}
	PRIVATE
		${PROJECT_SOURCE_DIR}/include
)

install(TARGETS ${CMAKE_PROJECT_NAME} DESTINATION build/bin)