cmake_minimum_required(VERSION 2.6)
project(test_coverage)

include(CTest)
enable_testing()
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set (CMAKE_BUILD_TYPE Debug)

add_executable(coverage coverage.cpp)
target_link_libraries(coverage gcov -fprofile-arcs -ftest-coverage)

add_test(NAME coverage COMMAND coverage)

include(CodeCoverage.cmake)
APPEND_COVERAGE_COMPILER_FLAGS()
SETUP_TARGET_FOR_COVERAGE_LCOV(
  NAME code_coverage
  EXECUTABLE ctest -j ${n_cores} # Executable in PROJECT_BINARY_DIR
  DEPENDENCIES
  coverage)
