# Range of versions. Highest possible will be set.
cmake_minimum_required(VERSION 3.14...3.18)

project(myProject VERSION 1.0 DESCRIPTION "Early alpha version." LANGUAGES CXX)

add_executable(Main main.cpp)


# this can be build with commands:

# 1)
# cmake -S . -B build
# cmake --build build

# 2) 
# mkdir build
# cd build
# cmake-gui ..
# Configure -> Generate
# ninja / make

# 3) 
# mkdir build
# cd build
# ccmake ..
# make