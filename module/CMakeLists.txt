message(STATUS "Start configuration for submodules.")

file(GLOB ELEMENTS "*") #전체 항목 불러옴

foreach(ELEMENT ${ELEMENTS})
  #폴더이고 그 안에 cmakelists를 가지고 있다면 -> 라이브러리로 판단하고 추가해준다
  if(IS_DIRECTORY ${ELEMENT} AND EXISTS ${ELEMENT}/CMakeLists.txt)
    message("Start configuration for ${ELEMENT}.")
    add_subdirectory(${ELEMENT})
    message("Finish configuration for ${ELEMENT}.")
  endif()
endforeach()

message(STATUS "Finish configuration for submodules.\n")
