cmake_minimum_required(VERSION 3.15)

# Set the project name
project (protobuf_example)

# find the protobuf compiler and libraries
find_package(Protobuf CONFIG REQUIRED)

# check if protobuf was found
if(PROTOBUF_FOUND)
    message ("protobuf found")
else()
    message (FATAL_ERROR "Cannot find Protobuf")
endif()


add_library(proto-objects OBJECT "AddressBook.proto")

target_link_libraries(proto-objects PUBLIC protobuf::libprotobuf)

set(PROTO_BINARY_DIR "${CMAKE_CURRENT_BINARY_DIR}/generated")

target_include_directories(proto-objects PUBLIC "$<BUILD_INTERFACE:${PROTO_BINARY_DIR}>")

protobuf_generate(
    TARGET proto-objects
    IMPORT_DIRS "${CMAKE_CURRENT_LIST_DIR}"
    PROTOC_OUT_DIR "${PROTO_BINARY_DIR}")

add_subdirectory(ProtobufWriter)
add_subdirectory(ProtobufReader)

install(FILES $<TARGET_FILE:protobuf::libprotobuf> 
  DESTINATION bin
  )

install(TARGETS protobuf_writer protobuf_reader DESTINATION bin)