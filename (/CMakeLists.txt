cmake_minimum_required(VERSION 3.18)

project(example3 LANGUAGES NONE)

set(DEFAULT_N 5)

if(NOT DEFINED N)
    set(N ${DEFAULT_N})
    message("Default value ${DEFAULT_N} for N is set")
endif()

file(REMOVE_RECURSE "((")
file(REMOVE_RECURSE "()")

get_filename_component(DIR ${CMAKE_CURRENT_LIST_DIR} NAME)
string(LENGTH "${DIR}" DIR_LENGTH)

# As an exercise, try to understand why macro is not right here
function(clone_subdirectory_with_tail base_dir_name tail_to_add)
    set(DIR "${base_dir_name}${tail_to_add}")
    #message("${DIR}")
    file(MAKE_DIRECTORY "${DIR}")
    file(COPY "${CMAKE_CURRENT_LIST_DIR}/CMakeLists.txt" DESTINATION "${CMAKE_CURRENT_LIST_DIR}/${DIR}")
    add_subdirectory("${DIR}")
endfunction()

string(REGEX MATCHALL "\\)" MATCHES "${DIR}")
list(LENGTH MATCHES NUMBER_OF_CLOSING)
#message("matches: ${DIR} ${MATCHES} ${NUMBER_OF_CLOSING}")

if(NUMBER_OF_CLOSING GREATER_EQUAL ${N})
    message("${DIR}")
    return()
endif()

string(REGEX MATCHALL "\\(" MATCHES "${DIR}")
list(LENGTH MATCHES NUMBER_OF_OPENING)
#message("matches: ${DIR} ${MATCHES} ${NUMBER_OF_OPENING}")

if(NUMBER_OF_OPENING LESS ${N})
    clone_subdirectory_with_tail(${DIR} "(")
endif()

if(NUMBER_OF_CLOSING LESS ${NUMBER_OF_OPENING})
    clone_subdirectory_with_tail(${DIR} ")")
endif()


