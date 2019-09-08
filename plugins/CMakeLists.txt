file(GLOB PATHS "${CMAKE_CURRENT_SOURCE_DIR}/*")

foreach(PATH ${PATHS})
  if((NOT IS_DIRECTORY ${PATH}) OR (NOT EXISTS "${PATH}/CMakeLists.txt"))
    continue()
  endif()

  message("Add subdirectory: ${PATH}")
  add_subdirectory(${PATH})
endforeach()
