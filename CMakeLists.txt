cmake_minimum_required(VERSION 3.10)

set(vcpkg_libs_path /bin/vcpkg/installed/x64-windows)

add_library(uvLib_windows STATIC IMPORTED)

#set_target_properties(uvLib_windows PROPERTIES
#  IMPORTED_IMPLIB ${vcpkg_libs_path}/lib/uv.lib
#  IMPORTED_LOCATION ${vcpkg_libs_path}/bin/uv.dll 
#)

set_target_properties(uvLib_windows PROPERTIES
  IMPORTED_LOCATION ${vcpkg_libs_path}/lib/uv.lib 
)


add_library(uWebSocketsLib OBJECT IMPORTED)

file(GLOB uWebSocketsLib_obj_files "${CMAKE_SOURCE_DIR}/uWebSockets/uSockets/*.o")
set(uWebSocketsLib_includes "${CMAKE_SOURCE_DIR}/uWebSockets/uSockets/src")

set_property(TARGET uWebSocketsLib PROPERTY
  IMPORTED_OBJECTS ${uWebSocketsLib_obj_files}
)

project(WebsocketServer)

add_executable(wsrv wsrv/main.cpp)

#target_link_libraries(wsrv 
#  $<$<PLATFORM_ID:Windows>:uWebSocketsLib>
#)
#target_include_directories(wsrv PRIVATE 
#  $<$<PLATFORM_ID:Windows>:${uWebSocketsLib_includes}>)

target_link_libraries(wsrv 
  uWebSocketsLib 
  uvLib_windows
)
target_include_directories(wsrv PRIVATE ${uWebSocketsLib_includes}>)

#project(app1)
#
#add_executable(app1 app1/main.cpp)
