project(supmap)
cmake_minimum_required(VERSION 2.8)

aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR} src_supmap)
aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR}/basic src_basic)
aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR}/basic src_io)

IF(WIN32)
  add_library(supmap STATIC ${src_supmap} ${src_basic} ${src_io})
  set_target_properties(supmap PROPERTIES LINK_FLAGS "/NODEFAULTLIB:LIBCMTD" LINK_FLAGS_DEBUG "/NODEFAULTLIB:\"LIBCMT;LIBCMTD;MSVCRT\"")
  INSTALL(TARGETS supmap ARCHIVE DESTINATION lib)
ELSE(WIN32)
  add_library(supmap SHARED ${src_supmap} ${src_basic} ${src_io})
  INSTALL(TARGETS supmap LIBRARY DESTINATION lib)
ENDIF(WIN32)

#安装需要头文件.
file(GLOB_RECURSE includes_basic
	${CMAKE_CURRENT_SOURCE_DIR}/basic/*.h)

#安装需要头文件.
file(GLOB_RECURSE includes_io
	${CMAKE_CURRENT_SOURCE_DIR}/io/*.h)

#安装需要头文件.
file(GLOB_RECURSE includes_supmap
	${CMAKE_CURRENT_SOURCE_DIR}/*.h)

INSTALL(FILES ${includes_supmap}  DESTINATION include/)
INSTALL(FILES ${includes_basic}  DESTINATION include/basic)
INSTALL(FILES ${includes_io}  DESTINATION include/io)
