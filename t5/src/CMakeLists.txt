add_executable(curltest main.cpp)


# plan 1
#include_directories(/usr/include)
#target_link_libraries(curltest curl)

# plan 2
FIND_PACKAGE(CURL)
IF(CURL_FOUND)
    INCLUDE_DIRECTORIES(${CURL_INCLUDE_DIR})
    TARGET_LINK_LIBRARIES(curltest ${CURL_LIBRARY})
ELSE(CURL_FOUND)
    MESSAGE(FATAL_ERROR ”CURL library not found”)
ENDIF(CURL_FOUND)