# Add an executable
project(protobuf_writer)

add_executable(protobuf_writer
    main.cpp
    )

target_include_directories(protobuf_writer
    PUBLIC
    ${CMAKE_CURRENT_BINARY_DIR}
)

# link the exe against the libraries
target_link_libraries(protobuf_writer
    PUBLIC
    proto-objects
)

add_custom_command(TARGET protobuf_writer   # Replace your_target_name with the name of your target
    POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy
            $<TARGET_FILE:protobuf::libprotobuf>  # Assuming Protobuf target is named libprotobuf
            $<TARGET_FILE_DIR:protobuf_writer>   # Destination directory is the binary directory of your target
    COMMENT "Copying protobuf.dll to binary directory"
)