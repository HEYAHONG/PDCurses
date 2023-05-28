cmake_minimum_required(VERSION 3.13)

project(PDCursesCore C CXX ASM)

file(GLOB PDCURSESCORE_CXX_C_FILES *.c)
add_library(PDCursesCore  ${PDCURSESCORE_CXX_C_FILES})
target_include_directories(PDCursesCore BEFORE
PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/../ )
