#-----------------------------------------------------------------------------
# Include Directories
#-----------------------------------------------------------------------------
include_directories(${FASTBIT_SOURCE_DIR}/src)

#-----------------------------------------------------------------------------
# Tests
#-----------------------------------------------------------------------------
add_executable(inRange inRange.cpp)
target_link_libraries(inRange fastbit)

add_executable(jrf jrf.cpp)
target_link_libraries(jrf fastbit)

add_executable(readcsv readcsv.cpp)
target_link_libraries(readcsv fastbit)

add_executable(setqgen setqgen.cpp)
target_link_libraries(setqgen fastbit)

add_executable(smatch smatch.cpp)
target_link_libraries(smatch fastbit)

#add_test(inRange ${PROJECT_BINARY_DIR}/bin/inRange)
#add_test(jrf     ${PROJECT_BINARY_DIR}/bin/jrf)
#add_test(readcsv ${PROJECT_BINARY_DIR}/bin/readcsv)
#add_test(setqgen ${PROJECT_BINARY_DIR}/bin/setqgen)
#add_test(smatch  ${PROJECT_BINARY_DIR}/bin/smatch)
