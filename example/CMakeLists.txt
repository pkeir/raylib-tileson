find_package(raylib CONFIG REQUIRED)

# raylib-tileson-example
add_executable(raylib-tileson-example raylib-tileson-example.c)
target_link_libraries(raylib-tileson-example PUBLIC
    raylib
    raylib-tileson
)

if (UNIX)
    target_link_libraries(raylib-tileson-example PUBLIC m dl pthread)

    if (CMAKE_BUILD_TYPE MATCHES Debug)
        target_link_options(raylib-tileson-example PRIVATE -fsanitize=address)
        target_link_options(raylib-tileson-example PRIVATE -fsanitize=undefined)
    endif()
endif()

# Copy the resources
file(GLOB resources resources/*)
set(test_resources)
list(APPEND test_resources ${resources})
file(COPY ${test_resources} DESTINATION "resources/")
