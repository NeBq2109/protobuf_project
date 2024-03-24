# Add an executable
project(protobuf_reader)

add_executable(protobuf_reader
    main.cpp
    )

target_include_directories(protobuf_reader
    PUBLIC
    ${CMAKE_CURRENT_BINARY_DIR}
)

# link the exe against the libraries
target_link_libraries(protobuf_reader
    PUBLIC
    proto-objects
)

add_custom_command(TARGET protobuf_reader
    POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy
            $<TARGET_FILE:protobuf::libprotobuf>
            $<TARGET_FILE_DIR:protobuf_reader>
    COMMENT "Copying protobuf.dll to binary directory"
)