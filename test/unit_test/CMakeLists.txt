file(COPY ${KEPUB_TEST_FILE} DESTINATION ${CMAKE_CURRENT_BINARY_DIR})

file(GLOB_RECURSE KEPUB_TEST_SRC CONFIGURE_DEPENDS
     ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp)

find_package(Catch2 REQUIRED)

add_executable(${KEPUB_TEST_EXECUTABLE} ${MIMALLOC_OBJECT} ${KEPUB_TEST_SRC})
target_link_libraries(
  ${KEPUB_TEST_EXECUTABLE} PRIVATE ${KEPUB_LIBRARY} Catch2::Catch2WithMain
                                   fmt::fmt pugixml::pugixml klib::klib)

include(Catch)
catch_discover_tests(${KEPUB_TEST_EXECUTABLE} REPORTER compact)
