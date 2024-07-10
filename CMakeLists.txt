cmake_minimum_required(VERSION 3.28 FATAL_ERROR)

project(x509lint)

find_package(OpenSSL REQUIRED)
set(LIBS OpenSSL::Crypto)

if(CYGWIN)
    list(APPEND LIBS iconv)
endif()

set(SOURCES
    x509lint.c
    checks.c
    messages.c
    asn1_time.c
)

add_executable(x509lint ${SOURCES})

target_link_libraries(x509lint ${LIBS})

target_compile_options(x509lint PRIVATE
    $<$<CXX_COMPILER_ID:MSVC>:/Wall>
    $<$<CXX_COMPILER_ID:GNU,Clang,AppleClang>:-Wall>
)
