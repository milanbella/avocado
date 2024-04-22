cmake_minimum_required(VERSION 3.10)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(vcpkg_install_path /bin/vcpkg/installed/x64-windows)

add_library(uvLib_windows STATIC IMPORTED)
set_target_properties(uvLib_windows PROPERTIES
  IMPORTED_LOCATION ${vcpkg_install_path}/lib/uv.lib 
)
target_include_directories(uvLib_windows 
  INTERFACE ${vcpkg_install_path}/include
)

add_library(zlib_windows STATIC IMPORTED)
set_target_properties(zlib_windows PROPERTIES
  IMPORTED_LOCATION ${vcpkg_install_path}/lib/zlib.lib 
)
target_include_directories(zlib_windows 
  INTERFACE ${vcpkg_install_path}/include
)


add_library(uWebSocketsLib OBJECT IMPORTED)
file(GLOB uWebSocketsLib_obj_files "${CMAKE_SOURCE_DIR}/uWebSockets/uSockets/*.o")
set(uWebSocketsLib_includes 
  "${CMAKE_SOURCE_DIR}/uWebSockets/uSockets/src" 
  "${CMAKE_SOURCE_DIR}/uWebSockets/src"
)
set_property(TARGET uWebSocketsLib PROPERTY
  IMPORTED_OBJECTS ${uWebSocketsLib_obj_files}
)
target_include_directories(uWebSocketsLib 
  INTERFACE ${vcpkg_install_path}/include
)


project(WebsocketServer)

add_executable(wsrv wsrv/main.cpp)

target_link_libraries(wsrv 
  uWebSocketsLib 
  uvLib_windows
  zlib_windows
)
target_include_directories(wsrv PRIVATE ${uWebSocketsLib_includes})

#project(app1)
#
#add_executable(app1 app1/main.cpp)
