cmake_minimum_required(VERSION 3.31)
project(audio_analyzer)

set(CMAKE_CXX_STANDARD 20)

add_executable(audio_analyzer src/cli/main.cpp)
