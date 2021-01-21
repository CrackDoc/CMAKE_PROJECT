# CMakeList.txt: CMakeProject 的 CMake 项目，在此处包括源代码并定义
# 项目特定的逻辑。
#
cmake_minimum_required (VERSION 3.8)


STRING( REGEX REPLACE ".*/(.*)" "\\1" PROJECT_NAME ${CMAKE_CURRENT_SOURCE_DIR} ) 

# TODO 添加模块变量
set(_INC_PATH ${CMAKE_CURRENT_SOURCE_DIR}/../${PROJECT_NAME}/include)
set(_SRC_PATH ${CMAKE_CURRENT_SOURCE_DIR}/../${PROJECT_NAME}/src)
SET(CURL_PATH "D:/IDE/IDEVS2010/CURLx86")

# 添加执行EXE目录
aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR}/../${PROJECT_NAME}/include _INC_EXPATH)
aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR}/../${PROJECT_NAME}/src _SRC_EXPATH)

# 添加头文件的搜索目录
include_directories(${_INC_PATH})
include_directories(${_SRC_PATH})
include_directories(${CURL_PATH}/include)

# TODO EXE编译连接
add_executable (${PROJECT_NAME} ${_INC_EXPATH} ${_SRC_EXPATH})


#TIDO 添加lib文件的搜索目录
link_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}/../${PROJECT_NAME}/lib
    ${CMAKE_CURRENT_SOURCE_DIR}/../lib)
link_directories(${CURL_PATH}/lib)

#TODO 条件lib 文件
#link_libraries(libcurl.lib)

#TODO 连接lib 文件
target_link_libraries(${PROJECT_NAME} ${CURL_PATH}/lib/libcurl.lib)
# target_link_libraries(${PROJECT_NAME} ../mylib1.a ${PROJECT_NAME} ../mylib2.so)
# target_link_libraries(${PROJECT_NAME} ../mylib1.lib ${PROJECT_NAME} ../mylib2.so)


# 将源代码添加到此项目的可执行文件。
# add_executable (CMakeProject "${CMAKE_CURRENT_SOURCE_DIR}/../CMakeProject/src/CMakeProject.cpp" "${CMAKE_CURRENT_SOURCE_DIR}/../CMakeProject/include/CMakeProject.h")

# TODO: 如有需要，请添加测试并安装目标。
