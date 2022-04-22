cmake_minimum_required(VERSION 3.0)

project(solver_mega)

add_executable(${PROJECT_NAME} ${CMAKE_CURRENT_SOURCE_DIR}/solver_app/solve_app_.cpp)

target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/solver_lib
                                                  ${CMAKE_CURRENT_SOURCE_DIR}/formatter_ex)

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/formatter_ex formatter_ex)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/solver_lib solver)

file(GLOB_RECURSE SOURCES  *_.cpp)
file(GLOB_RECURSE INCLUDES *.h)
file(GLOB_RECURSE LIBS lib*.a)


target_link_libraries(${PROJECT_NAME} solver formatter_ex)

install(FILES ${SOURCES} DESTINATION src)
install(FILES ${INCLUDES} DESTINATION inc)

install(TARGETS formatter DESTINATION lib)
install(TARGETS formatter_ex DESTINATION lib)
install(TARGETS solver DESTINATION lib)
install(TARGETS ${PROJECT_NAME} DESTINATION bin)

set(CPACK_DEBIAN_PACKAGE_MAINTAINER "SOLVER")
include(CPack)
