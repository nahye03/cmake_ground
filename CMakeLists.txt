#최상단에 최소 버전을 작성해야함
cmake_minimum_required(VERSION 3.11) 

#프로젝트 이름과 버전 명시해야함함
set(PACKAGE_NAME CMAKE_GROUND) #프로젝트 네임
set(PACKAGE_VERSION 1.1.0)

# project는 cmake 만들 때 필수(적어도 이름, 버전, 언어)
project(
  ${PACKAGE_NAME}
  VERSION ${PACKAGE_VERSION}
  LANGUAGES CXX
  DESCRIPTION "CMake Ground") #프로젝트 버전, 언어 설정

#------------------For문 Test--------------------
# if는 반드시 endif랑 써야함
# set(BOOL_VAL1 TRUE)
# set(BOOL_VAL2 TRUE)
# if(BOOL_VAL1 AND BOOL_VAL2)
#   message(STATUS "BOOL_VAL1 AND BOOL_VAL2 is TRUE")
# elseif(NOT BOOL_VAL2)
#   message(STATUS "BOOL_VAL2 is FALSE")
# else()
#   message(STATUS "BOOL_VAL1 AND BOOL_VAL2 is FALSE")
# endif()

# set(STRING_1 "STRIGN_1")
# set(STRING_2 "STRIGN_1")
# if(STRING_1 STREQUAL STRING_2)
#   message(STATUS "caes 1")
# else()
#   message(STATUS "case 2")
# endif()
#-------------------------------------------------

#-----------------foreach Test--------------------
# set(LIST_1 "0" "1" "2" "3" "4" "5")
# foreach(VAR IN LISTS LIST_1)
#   message(STATUS "VAR: ${VAR}")
# endforeach()
#-------------------------------------------------

#-----------------Message Test--------------------
# message(STATUS "PROJECT_NAME : ${PROJECT_NAME}") #project_name을 선언하지 않았지만 project 명령어를 통해 이름이 정해짐
# message(STATUS "PROJECT_VERSION_MAJOR : ${PROJECT_VERSION_MAJOR}") #버전의 맨 앞 수
# message(STATUS "PROJECT_VERSION_MINOR : ${PROJECT_VERSION_MINOR}") #버전 가운데 수
# message(STATUS "PROJECT_VERSION_PATCH : ${PROJECT_VERSION_PATCH}") #버전 맨 뒤 수
# message(STATUS "PROJECT_DESCRIPTION : ${PROJECT_DESCRIPTION}")

# message(STATUS "PROJECT_SOURCE_DIR : ${PROJECT_SOURCE_DIR}") #해당 프로젝스 소스 절대 경로(자동으로 만들어진다)
# message(STATUS "PROJECT_BINARY_DIR : ${PROJECT_BINARY_DIR}") #해당 프로젝스 빌드 위치(자동으로 만들어진다)


# set(STRING_VARIABLE "Hello World")
# set(BOOL_VARIABLE TRUE)

# message(STATUS "[Status] STRING_VARIABLE: ${STRING_VARIABLE}")
# message(STATUS "BOOL_VARIABLE : ${BOOL_VARIABLE}")

# message(WARNING "[WARNING] STRING_VARIABLE: ${STRING_VARIABLE}") #에러 메시지 출력
# message(FATAL_ERROR "[FATAL_ERROR] STRING_VARIABLE: ${STRING_VARIABLE}") #에러가 뜨면서 종료됨
# message(SEND_ERROR "[SEND_ERROR] STRING_VARIABLE: ${STRING_VARIABLE}") #에러가 뜨지만 종료되지는 않음
# message(DEPRECATION "[DEPRECATION] STRING_VARIABLE: ${STRING_VARIABLE}")


# add_subdirectory(example) #example 아래에 있는 cmakelist 실행

# message(STATUS "[Status] GLOBAL_STRING_VARIABLE: ${GLOBAL_STRING_VARIABLE}") #example의 전역변수 불러옴
# message(STATUS "[Status] GLOBAL_BOOL_VARIABLE : ${GLOBAL_BOOL_VARIABLE}")
#-------------------------------------------------


set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)

set(${PACKAGE_NAME}_PATH ${CMAKE_CURRENT_SOURCE_DIR})
set(${PACKAGE_NAME}_SOURCE_PATH "${${PACKAGE_NAME}_PATH}/src")
set(${PACKAGE_NAME}_INCLUDE_PATH "${${PACKAGE_NAME}_PATH}/include")
set(${PACKAGE_NAME}_TEST_PATH "${${PACKAGE_NAME}_PATH}/test")
set(${PACKAGE_NAME}_RESOURCE_PATH "${${PACKAGE_NAME}_PATH}/resource")
set(${PACKAGE_NAME}_MODULE_PATH "${${PACKAGE_NAME}_PATH}/module")
set(${PACKAGE_NAME}_THIRDPARTY_PATH "${${PACKAGE_NAME}_PATH}/thirdparty")

message(STATUS "PACKAGE_NAME: ${PACKAGE_NAME}")
message(STATUS "PACKAGE_NAME: ${PACKAGE_VERSION}")
message(STATUS "${PACKAGE_NAME}_PATH: ${${PACKAGE_NAME}_PATH}")
message(STATUS "${PACKAGE_NAME}_SOURCE_PATH: ${${PACKAGE_NAME}_SOURCE_PATH}")
message(STATUS "${PACKAGE_NAME}_INCLUDE_PATH: ${${PACKAGE_NAME}_INCLUDE_PATH}")
message(STATUS "${PACKAGE_NAME}_TEST_PATH: ${${PACKAGE_NAME}_TEST_PATH}")
message(STATUS "${PACKAGE_NAME}_RESOURCE_PATH: ${${PACKAGE_NAME}_RESOURCE_PATH}")
message(STATUS "${PACKAGE_NAME}_MODULE_PATH: ${${PACKAGE_NAME}_MODULE_PATH}")
message(STATUS "${PACKAGE_NAME}_THIRDPARTY_PATH: ${${PACKAGE_NAME}_THIRDPARTY_PATH}\n")

add_subdirectory(${${PACKAGE_NAME}_THIRDPARTY_PATH}) #외부 모듈 라이브러리
add_subdirectory(${${PACKAGE_NAME}_MODULE_PATH}) # 내가 만든 라이브러리

# main을 실행할 때 target library를 추가해줌
add_executable(MAIN src/main.cpp)
target_link_libraries(MAIN
  CMAKE_GROUND_EXAMPLE #_MODULE_PATH에서 만든 library
)

target_compile_options(MAIN PRIVATE
  -Wall -Wextra -Wpedantic -Werror
)
