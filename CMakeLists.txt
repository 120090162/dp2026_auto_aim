cmake_minimum_required(VERSION 3.12)
project(DPAUTOAIM-RM2026)

# 设置编译指令
set(CMAKE_CXX_STANDARD 17)
# Export compile commands for clang-tidy
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
# set(CMAKE_BUILD_TYPE DEBUG)
# add_compile_options(-g -O0 -w -fno-omit-frame-pointer -Wno-notes)
set(CMAKE_BUILD_TYPE RELEASE)
add_compile_options(-O3 -w)

# 使用ccache提高编译速度
find_program(CCACHE_FOUND ccache)
if(CCACHE_FOUND)
    message(STATUS "Set up ccache ...")
    set_property(GLOBAL PROPERTY RULE_LAUNCH_COMPILE ccache)
    set_property(GLOBAL PROPERTY RULE_LAUNCH_LINK ccache)
endif()

# 开启 Interprocedural optimization
include(CheckIPOSupported)
check_ipo_supported(RESULT _IsIPOSupported)
    if(_IsIPOSupported)
    message(STATUS "Turn on INTERPROCEDURAL_OPTIMIZATION")
    set(CMAKE_INTERPROCEDURAL_OPTIMIZATION TRUE)
endif()

# 设置目标兵种
# add_definitions(-DDPAUTOAIM_HERO)
add_definitions(-DDPAUTOAIM_INFANTRY)
# add_definitions(-DDPAUTOAIM_BALANCE)
# add_definitions(-DDPAUTOAIM_SENTRY)
# add_definitions(-DDPAUTOAIM_DRONSE)

# CUDA
find_package(CUDA REQUIRED)
include_directories(/usr/local/cuda/include)

# DPRM
find_package(DPRM REQUIRED)
include_directories(${DPRM_INCLUDE_DIRS})

# OpenCV
find_package(OpenCV 4.10.0 REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})

# Eigen
find_package(Eigen3 REQUIRED)
include_directories(${EIGEN3_INCLUDE_DIR})

# Ceres
find_package(Ceres REQUIRED)
include_directories(${CERES_INCLUDE_DIRS})


# 添加项目头文件
include_directories(${CMAKE_SOURCE_DIR}/include)

# 添加构建子目录
add_subdirectory(src/data_manager)
add_subdirectory(src/garage)
add_subdirectory(src/threads)


# 添加可执行文件
add_executable(DPAUTOAIM-RM2026 src/main.cpp)


# 链接模块静态库
target_link_libraries(DPAUTOAIM-RM2026
    data_manager
    garage
    threads
)

install(TARGETS DPAUTOAIM-RM2026
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib)
