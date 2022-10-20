cmake_minimum_required(VERSION 3.16)
project(reorder CXX)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_C_STANDARD 99)

set(CMAKE_CXX_FLAGS "-Wall -Wextra -Wcast-align -Wcast-qual -Wconversion -Wfloat-equal -Wformat=2 -Winit-self -Wmissing-declarations -Wmissing-include-dirs -Wpointer-arith -Wredundant-decls -Wswitch-default -Wuninitialized -Wwrite-strings -Wno-sign-conversion -Wno-unused-function -Wno-missing-declarations -fopenmp -std=c++14 -mcx16 -O3 -DNDEBUG ")

add_compile_options(-l sqlite3)

find_package(Boost 1.58.0 COMPONENTS system filesystem graph serialization REQUIRED)

set(GraphPreprocessDir "/home/atrostan/Workspace/repos/congenial-enigma/graph_preprocess")


add_executable(reorder  ../../graph_preprocess/sql.h ../../graph_preprocess/sql.cpp reorder.cc ../rabbit_order.hpp edge_list.hpp )
target_include_directories(reorder PUBLIC ${GraphPreprocessDir})

link_directories(${GraphPreprocessDir})
target_link_libraries(reorder LINK_PUBLIC sqlite3 ${Boost_LIBRARIES} tcmalloc_minimal numa )
