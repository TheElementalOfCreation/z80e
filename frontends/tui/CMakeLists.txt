cmake_minimum_required(VERSION 2.8)
project (tui)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "bin/")
include_directories(SYSTEM ${CMAKE_CURRENT_SOURCE_DIR}/../../libz80e/include)

list(INSERT CMAKE_MODULE_PATH 0 ${CMAKE_CURRENT_SOURCE_DIR}/../../CMake)
find_package(Scas REQUIRED)

add_executable(z80e-tui
	main.c
	tui.c
	$<TARGET_OBJECTS:z80e_objects>
)

TARGET_LINK_LIBRARIES(z80e-tui readline)

if(NOT APPLE AND NOT HAIKU)
	TARGET_LINK_LIBRARIES(z80e-tui rt)
endif()
TARGET_LINK_LIBRARIES(z80e-tui ${SCAS_LIBRARIES})


INSTALL(TARGETS z80e-tui
	RUNTIME DESTINATION bin)
