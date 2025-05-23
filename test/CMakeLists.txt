cmake_minimum_required(VERSION 3.14)

project(subprocessTests LANGUAGES CXX)

include(../cmake/project-is-top-level.cmake)
include(../cmake/windows-set-path.cmake)

if(PROJECT_IS_TOP_LEVEL)
  find_package(subprocess REQUIRED)
  enable_testing()
endif()

add_executable(subprocess_test source/subprocess_test.cpp)
target_link_libraries(subprocess_test PRIVATE
    subprocess::subprocess
)
target_include_directories(subprocess_test PUBLIC
  ${CMAKE_CURRENT_SOURCE_DIR}/third_party
)
target_compile_features(subprocess_test PRIVATE cxx_std_17)
set_target_properties(subprocess_test
  PROPERTIES CXX_CLANG_TIDY ""
)

add_test(NAME subprocess_test COMMAND subprocess_test)
windows_set_path(subprocess_test subprocess::subprocess)
