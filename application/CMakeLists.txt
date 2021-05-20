# build all examples into the bin directory
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/bin)

find_package(vsg REQUIRED)

# find the optional vsgXchange that can be used for reading and range of image and 3d model formats and shader compilation
find_package(vsgXchange QUIET)

set(SOURCES
    main.cpp
)

add_executable(myvsgapplication ${SOURCES})

target_link_libraries(myvsgapplication vsg::vsg)

if (vsgXchange_FOUND)
    target_compile_definitions(myvsgapplication PRIVATE vsgXchange_FOUND)
    target_link_libraries(myvsgapplication vsgXchange::vsgXchange)
endif()

install(TARGETS myvsgapplication
        RUNTIME DESTINATION bin
)
