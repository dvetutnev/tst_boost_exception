project(tst_boost_exception CXX)
cmake_minimum_required(VERSION 3.0)


include(conan.cmake)
conan_cmake_run(
    REQUIRES
        boost/[>=1.67.0]@odant/stable
        BASIC_SETUP
        CMAKE_TARGETS
        NO_OUTPUT_DIRS
        UPDATE
        BUILD
            outdated
        IMPORTS
            "bin, *.dll -> ./bin"
            "bin, *.pdb -> ./bin"
            "lib, *.so* -> ./bin"
)

find_package(Boost REQUIRED exception)

enable_testing()

add_executable(main main.cpp)
target_link_libraries(main Boost::exception)
add_test(
    NAME main
    COMMAND main
    WORKING_DIRECTORY ${CMAKE_BINARY_DIR}/bin
)
set_property(TEST main PROPERTY TIMEOUT 100)
