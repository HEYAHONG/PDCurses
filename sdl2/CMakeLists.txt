cmake_minimum_required(VERSION 3.13)
set(PDCURSESLIB PDCursesSDL2)
project(${PDCURSESLIB} C CXX ASM)
file(GLOB PD_C_FILES pd*.c)
add_library(${PDCURSESLIB}  ${PD_C_FILES})
target_include_directories(${PDCURSESLIB} BEFORE
PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/ 
PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/../
)

option(DEBUG "PDCDEBUG" OFF)
if(DEBUG)
target_compile_definitions(${PDCURSESLIB} PUBLIC "-DPDCDEBUG")
endif()
option(WIDE "PDC_WIDE" OFF)
if(WIDE)
target_compile_definitions(${PDCURSESLIB} PUBLIC "-DPDC_WIDE")
target_link_libraries(${PDCURSESLIB} SDL2_ttf)
endif()
option(UTF8 "PDC_FORCE_UTF8" ON)
if(UTF8)
target_compile_definitions(${PDCURSESLIB} PUBLIC "-DPDC_FORCE_UTF8")
endif()

#PDCursesCore链接
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../pdcurses pdcurses)
target_link_libraries(PDCursesCore ${PDCURSESLIB})

include(FindPkgConfig)
#链接SDL2
pkg_check_modules(SDL2 REQUIRED IMPORTED_TARGET sdl2)
target_link_libraries(${PDCURSESLIB} PkgConfig::SDL2)

#添加Demos
set(DEMOS_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../demos/)

add_executable(firework ${DEMOS_DIR}/firework.c )
target_link_libraries(firework PDCursesCore)

add_executable(ozdemo  ${DEMOS_DIR}/ozdemo.c )
target_link_libraries(ozdemo PDCursesCore)

add_executable(ptest  ${DEMOS_DIR}/ptest.c )
target_link_libraries(ptest PDCursesCore)

add_executable(rain  ${DEMOS_DIR}/rain.c )
target_link_libraries(rain PDCursesCore)

add_executable(testcurs  ${DEMOS_DIR}/testcurs.c )
target_link_libraries(testcurs PDCursesCore)

add_executable(tuidemo  ${DEMOS_DIR}/tuidemo.c  ${DEMOS_DIR}/tui.c )
target_link_libraries(tuidemo PDCursesCore)

add_executable(worm  ${DEMOS_DIR}/worm.c )
target_link_libraries(worm PDCursesCore)

add_executable(xmas  ${DEMOS_DIR}/xmas.c )
target_link_libraries(xmas PDCursesCore)

add_executable(sdltest  sdltest.c )
target_link_libraries(sdltest PDCursesCore)
