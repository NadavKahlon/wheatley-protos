cmake_minimum_required(VERSION 3.10)
project(aperture_protos VERSION 0.1.0)


find_package(Protobuf REQUIRED)

# Add target to compile `aperture_protos.lib` using all `.proto` files
file(GLOB_RECURSE PROTO_FILES "${CMAKE_CURRENT_SOURCE_DIR}/*.proto")
add_library(${PROJECT_NAME} STATIC ${PROTO_FILES})

# Run `protoc` and add generated sources to target
protobuf_generate(
    TARGET ${PROJECT_NAME}
    PROTOC_OUT_DIR "${CMAKE_CURRENT_BINARY_DIR}"
)

# Link against Protobuf library
target_link_libraries(${PROJECT_NAME} PUBLIC protobuf::libprotobuf)

# Make generated headers public
target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_BINARY_DIR})
