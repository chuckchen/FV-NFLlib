cmake_minimum_required(VERSION 3.12)

project(FV-NFLlib CXX)

set(CMAKE_CXX_STANDARD 11)
add_compile_options(-funroll-loops -Ofast -Wall -g)

if(NOT NFLLIB_DIR)
    set(NFLLIB_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../NFLlib)
endif()

add_subdirectory(${NFLLIB_DIR} ${NFLLIB_DIR}/build EXCLUDE_FROM_ALL)

include_directories(${CMAKE_CURRENT_SOURCE_DIR} ${NFLLIB_DIR}/include)

enable_testing()

set(TEST_DIR ${CMAKE_CURRENT_SOURCE_DIR}/tests)

add_executable(Test_binary_tree ${TEST_DIR}/Test_binary_tree.cpp)
target_link_libraries(Test_binary_tree nfllib ${GMP_LIBRARY} ${MPFR_LIBRARY})
add_test(NAME Test_binary_tree COMMAND Test_binary_tree)

add_executable(Test_ec_additions ${TEST_DIR}/Test_ec_additions.cpp)
target_link_libraries(Test_ec_additions nfllib ${GMP_LIBRARY} ${MPFR_LIBRARY})
add_test(NAME Test_ec_additions COMMAND Test_ec_additions)

add_executable(Test_Kreyvium ${TEST_DIR}/Test_Kreyvium.cpp)
target_link_libraries(Test_Kreyvium nfllib ${GMP_LIBRARY} ${MPFR_LIBRARY})
add_test(NAME Test_Kreyvium COMMAND Test_Kreyvium)

add_executable(Test_poly_encrypt ${TEST_DIR}/Test_poly_encrypt.cpp)
target_link_libraries(Test_poly_encrypt nfllib ${GMP_LIBRARY} ${MPFR_LIBRARY})
add_test(NAME Test_poly_encrypt COMMAND Test_poly_encrypt)

add_executable(Test_simple ${TEST_DIR}/Test_simple.cpp)
target_link_libraries(Test_simple nfllib ${GMP_LIBRARY} ${MPFR_LIBRARY})
add_test(NAME Test_simple COMMAND Test_simple)