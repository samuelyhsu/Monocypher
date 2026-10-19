# Static library for use through add_subdirectory().
# Includes the optional Ed25519 module (RFC 8032, SHA-512); the core
# library's crypto_eddsa_* functions use BLAKE2b instead.
cmake_minimum_required(VERSION 3.10...3.31)
project(monocypher LANGUAGES C)

add_library(
    monocypher
    STATIC
    src/monocypher.c
    src/monocypher.h
    src/optional/monocypher-ed25519.c
    src/optional/monocypher-ed25519.h
)
target_include_directories(monocypher PUBLIC src src/optional)
if(MSVC)
    # crypto_argon2_init() declares a local blake2b ctx that shadows its ctx
    # parameter; harmless, and /W4 would flag it in every parent build.
    target_compile_options(monocypher PRIVATE /wd4457)
endif()
