set(TARGET_NAME SprocketApp)

file(GLOB SOURCE_FILES *.cpp *.h)

include_directories("../")

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOMOC ON)
FIND_PACKAGE(Qt5 COMPONENTS Core REQUIRED)

SET(SrcRccs "resources/darkstyle.qrc")
QT5_ADD_RESOURCES(SrcRccsSrc ${SrcRccs})

SET(SOURCE_FILES ${SOURCE_FILES} ${SrcRccsSrc})
SOURCE_GROUP("Generated Ui Files" FILES ${SrcRccsSrc})

add_executable(${TARGET_NAME} ${SOURCE_FILES} ${HEADER_FILES})
target_link_libraries (${TARGET_NAME} Sprocket)

target_compile_definitions(${TARGET_NAME} PRIVATE CMAKE_BINARY_DIR=${CMAKE_BINARY_DIR})

SET( CMAKE_EXE_LINKER_FLAGS  "${CMAKE_EXE_LINKER_FLAGS} /FORCE:MULTIPLE" )# TODO: fix

if(WIN32)
    set_target_properties(${TARGET_NAME} PROPERTIES LINK_FLAGS_DEBUG "/SUBSYSTEM:CONSOLE")
	set_target_properties(${TARGET_NAME} PROPERTIES LINK_FLAGS_RELEASE "/SUBSYSTEM:CONSOLE")
	set_target_properties(${TARGET_NAME} PROPERTIES LINK_FLAGS_MINSIZEREL "/SUBSYSTEM:CONSOLE")
	set_target_properties(${TARGET_NAME} PROPERTIES LINK_FLAGS_RELWITHDEBINFO "/SUBSYSTEM:CONSOLE")
endif()
