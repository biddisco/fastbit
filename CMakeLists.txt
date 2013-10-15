PROJECT(FASTBIT)

cmake_minimum_required(VERSION 2.8)

set(CMAKE_MODULE_PATH "${FASTBIT_SOURCE_DIR}" ${CMAKE_MODULE_PATH})

#--------------------------------------------------
# Setup Output directories
#--------------------------------------------------
SET (CMAKE_RUNTIME_OUTPUT_DIRECTORY
    ${PROJECT_BINARY_DIR}/bin CACHE PATH "Single Directory for all Executables."
)
SET (CMAKE_LIBRARY_OUTPUT_DIRECTORY
    ${PROJECT_BINARY_DIR}/bin CACHE PATH "Single Directory for all Libraries"
)
SET (CMAKE_ARCHIVE_OUTPUT_DIRECTORY
    ${PROJECT_BINARY_DIR}/bin CACHE PATH "Single Directory for all static libraries."
)

SET(FASTBIT_TEST_DIR ${PROJECT_BINARY_DIR}/Testing/Temporary)
#--------------------------------------------------
# Testing : Include the standard testing module
#--------------------------------------------------------
INCLUDE(${CMAKE_ROOT}/Modules/CTest.cmake)

#-----------------------------------------------------------------------------
# Thread library
#-----------------------------------------------------------------------------
if(WIN32)
  # creates Threads_INCLUDE_DIR, Threads_PTHREADWIN32_LIBRARY cache vars 
  # sets CMAKE_THREAD_LIBS_INIT accordingly
  set(THREADS_USE_PTHREADS_WIN32 true)
endif(WIN32)

find_package(Threads REQUIRED)
message("CMAKE_THREAD_LIBS_INIT is ${CMAKE_THREAD_LIBS_INIT}")
include_directories(${THREADS_PTHREADS_INCLUDE_DIR})

#-----------------------------------------------------------------------------
# subdirs
#-----------------------------------------------------------------------------
add_subdirectory(src)
add_subdirectory(examples)
add_subdirectory(tests)
