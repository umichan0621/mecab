cmake_minimum_required(VERSION 3.5)
project(mecab)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14 -Wall -fPIC -O2")

set(SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/mecab/src)

add_definitions(-DVERSION="0.996")
add_definitions(-DMECAB_DEFAULT_RC="mecabrc")
add_definitions(-DPACKAGE="mecab")
add_definitions(-DDIC_VERSION=102)
add_definitions(-D_WIN32_IE=0x0900)
add_definitions(-DMECAB_USE_THREAD -D_CRT_SECURE_NO_DEPRECATE -DHAVE_WINDOWS_H -DDLL_EXPORT -DHAVE_GETENV -DUNICODE -D_UNICODE)

include_directories(
    ${SOURCE_DIR}
)

file(GLOB SRC_FILES
    ${SOURCE_DIR}/libmecab.cpp
    ${SOURCE_DIR}/tagger.cpp
    ${SOURCE_DIR}/nbest_generator.cpp
    ${SOURCE_DIR}/string_buffer.cpp
    ${SOURCE_DIR}/writer.cpp
    ${SOURCE_DIR}/viterbi.cpp
    ${SOURCE_DIR}/utils.cpp
    ${SOURCE_DIR}/param.cpp
    ${SOURCE_DIR}/eval.cpp
    ${SOURCE_DIR}/iconv_utils.cpp
    ${SOURCE_DIR}/dictionary_rewriter.cpp
    ${SOURCE_DIR}/dictionary_generator.cpp
    ${SOURCE_DIR}/dictionary_compiler.cpp
    ${SOURCE_DIR}/context_id.cpp
    ${SOURCE_DIR}/connector.cpp
    ${SOURCE_DIR}/char_property.cpp
    ${SOURCE_DIR}/dictionary.cpp
    ${SOURCE_DIR}/feature_index.cpp
    ${SOURCE_DIR}/lbfgs.cpp
    ${SOURCE_DIR}/learner_tagger.cpp
    ${SOURCE_DIR}/learner.cpp
    ${SOURCE_DIR}/tokenizer.cpp
)

add_library(${PROJECT_NAME} SHARED 
    ${SRC_FILES})

add_executable(${PROJECT_NAME}_example 
    mecab/example/example.cpp)

target_link_libraries(${PROJECT_NAME}_example 
    ${PROJECT_NAME})

install(DIRECTORY ${SOURCE_DIR}/
    DESTINATION include/${PROJECT_NAME} 
    FILES_MATCHING 
    PATTERN "mecab.h")

install(TARGETS ${PROJECT_NAME}
    LIBRARY DESTINATION lib)