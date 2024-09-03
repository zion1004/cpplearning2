cmake_minimum_required(VERSION 3.28)

project(hello_world LANGUAGES CXX)

add_executable(hello_world src/main.cpp)

set(MYVAR "hello world!")

# variables are scoped
function(print)
    foreach(var ${ARGN})
        message("${var} = ${${var}}")
    endforeach()
    set(MYVAR "no longer say hello")
endfunction()

function(print_env)
    foreach(var ${ARGN})
        message("${var} = $ENV{${var}}")
    endforeach()
    set(MYVAR "no longer say hello")
endfunction()

# macros are inlined and can affect variables outside of its "scope"
macro(printmacro)
    foreach(var ${ARGN})
        message("${var} = ${${var}}")
    endforeach()
    set(MYVAR "no longer say hello")
endmacro()

print(PROJECT_NAME PROJECT_NAME_FOO MYVAR)
print(MYVAR)
printmacro(MYVAR)
printmacro(MYVAR)

print_env(PROJECT_NAME PROJECT_NAME_FOO MYVAR)
