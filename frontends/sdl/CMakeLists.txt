cmake_minimum_required(VERSION 2.8)
project (sdl)

list(INSERT CMAKE_MODULE_PATH 0 ${CMAKE_CURRENT_SOURCE_DIR}/../../CMake)
find_package(SDL REQUIRED)
find_package(Scas REQUIRED)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "bin/")
include_directories(SYSTEM ${CMAKE_CURRENT_SOURCE_DIR}/../../libz80e/include)

add_executable(z80e-sdl
	main.c
	tui.c
	$<TARGET_OBJECTS:z80e_objects>
)

TARGET_LINK_LIBRARIES(z80e-sdl readline ${SDL_LIBRARY})

if(NOT APPLE AND NOT HAIKU)
	TARGET_LINK_LIBRARIES(z80e-sdl rt)
endif()
TARGET_LINK_LIBRARIES(z80e-sdl ${SCAS_LIBRARIES})

INSTALL(TARGETS z80e-sdl
	RUNTIME DESTINATION bin)