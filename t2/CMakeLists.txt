project(HELLO)

add_subdirectory(src bin)

install(FILES COPYRIGHT readme.md DESTINATION share/doc/cmake/t2)

install(PROGRAMS runhello.sh DESTINATION bin)

install(DIRECTORY doc/ DESTINATION share/doc/cmake/t2)