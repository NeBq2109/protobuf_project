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

add_custom_command(TARGET protobuf_reader   # Replace your_target_name with the name of your target
    POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy
            $<TARGET_FILE:protobuf::libprotobuf>  # Assuming Protobuf target is named libprotobuf
            $<TARGET_FILE_DIR:protobuf_reader>   # Destination directory is the binary directory of your target
    COMMENT "Copying protobuf.dll to binary directory"
)