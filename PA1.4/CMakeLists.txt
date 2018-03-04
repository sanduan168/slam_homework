cmake_minimum_required(VERSION 3.5)
project(Hello)

IF (NOT CMAKE_BUILD_TYPE)
    SET(CMAKE_BUILD_TYPE Release)
ENDIF ()
message("Build type: " ${CMAKE_BUILD_TYPE})

set(CMAKE_CXX_STANDARD 11)

#config header path
include_directories(${PROJECT_SOURCE_DIR}/include)

#config shared lib
set(LIB_NAME hello)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/lib)
add_library(${LIB_NAME} SHARED src/hello.cpp)

#config install path
set(CMAKE_INSTALL_PREFIX /usr/local/)
install(FILES include/hello.h DESTINATION include)
install(TARGETS ${LIB_NAME} LIBRARY DESTINATION lib)

#config bin
add_executable(sayhello useHello.cpp)
target_link_libraries(sayhello ${LIB_NAME})