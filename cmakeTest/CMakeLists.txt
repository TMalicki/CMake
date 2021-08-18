cmake_minimum_required(VERSION 3.9.1)

project(CMakeHello)

set(CMAKE_CXX_STANDARD 14)

# check system type
##############################

# UNIX, WIN32, WINRT, CYGWIN, APPLE are environment variables as flags set by default system
if(UNIX)
    message("This is a ${CMAKE_SYSTEM_NAME} system")
elseif(WIN32)
    message("This is a Windows System")
endif()
# or use MATCHES to see if actual system name 
# Darwin is Apple's system name
if(${CMAKE_SYSTEM_NAME} MATCHES Darwin)
    message("This is a ${CMAKE_SYSTEM_NAME} system")
elseif(${CMAKE_SYSTEM_NAME} MATCHES Windows)
    message("This is a Windows System")
endif()

##############################




# define makro for system type
###############################

# or use MATCHES to see if actual system name 
# Darwin is Apple's system name
if(${CMAKE_SYSTEM_NAME} MATCHES Darwin)
    add_definitions(-DMACROSAMPLE="Apple MacOS")
elseif(${CMAKE_SYSTEM_NAME} MATCHES Windows)
    add_definitions(-DMACROSAMPLE="Windows PC")
endif()

###############################




# generate binary files in /bin folder
###############################

#set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR}/bin)

###############################





# generate .exe binary without libraries
###############################

# add_executable(cmake_hello main.cpp)




# generate .exe binary with libraries with Target
################################

# add_executable(cmake_hello main.cpp lib/math/operations.cpp lib/math/operations.hpp)

# alternatively:
# set(SOURCES main.cpp
#             lib/math/operations.cpp
#             lib/math/operations.hpp)
# add_executable(cmake_hello ${SOURCES})




# generate .exe binary seperately from library, and linking them together
#################################

# set(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR}/lib)

# add_library(math SHARED lib/math/operations.cpp)
# or:
# add_library(math STATIC lib/math/operations.cpp)

# add_executable(cmake_hello main.cpp)
# target_link_libraries(cmake_hello math)
#lib folder has to be added to the system (user) path




# generate .exe binary normaly and library as sub-module
#################################

# add_subdirectory(lib/math)
# add_executable(cmake_hello main.cpp)
# target_link_libraries(cmake_hello math)





# find_package
###################################

add_executable(cmake_hello main.cpp)
add_subdirectory(lib/math)
target_link_libraries(cmake_hello math)

find_package(Boost 1.66)
# Check for libray, if found print message, include dirs and link libraries.
if(Boost_FOUND)
    message("Boost Found")
    include_directories(${Boost_INCLUDE_DIRS})
    target_link_libraries(cmake_hello ${Boost_LIBRARIES})
elseif(NOT Boost_FOUND)
    error("Boost Not Found")
endif()

