set(c_options "")
if(MSVC)
  #..
elseif("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
  list(APPEND c_options "-pthread")
elseif("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
  list(APPEND c_options "-pthread")
endif()
set(l_options "")
if(MSVC)
  #..
elseif("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
  list(APPEND l_options "-lpthread")
elseif("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
  list(APPEND l_options "-lpthread")
endif()

Ubpa_AddTarget(
  MODE STATIC
  RET_TARGET_NAME tname
  SOURCE
    "${PROJECT_SOURCE_DIR}/include/UECS"
  LIB
    Ubpa::UTemplate_core
    Ubpa::UGraphviz_core
  INC
    "${PROJECT_SOURCE_DIR}/include"
  C_OPTION
    ${c_options}
  L_OPTION
    ${l_options}
)

target_precompile_headers(${tname} PRIVATE "${PROJECT_SOURCE_DIR}/include/UECS/World.h")
