# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

# Sets the minimum version of CMake required to build the native library.
cmake_minimum_required(VERSION 3.10)
#定义.so .a文件的路径
set(distribution_DIR ${CMAKE_SOURCE_DIR}/src/main/cpp)

include_directories(${CMAKE_SOURCE_DIR}/src/main/cpp/ffmpeg/include)
include_directories(${CMAKE_SOURCE_DIR}/src/main/cpp/faac/include)
include_directories(${CMAKE_SOURCE_DIR}/src/main/cpp/librtmp/include)
include_directories(${CMAKE_SOURCE_DIR}/src/main/cpp/x264/include)

#加载FFmpeg库
add_library( avcodec-57
        SHARED
        IMPORTED )
set_target_properties( avcodec-57
        PROPERTIES IMPORTED_LOCATION
        ${distribution_DIR}/ffmpeg/libs/libavcodec-57.so )

add_library( avdevice-57
        SHARED
        IMPORTED )
set_target_properties( avdevice-57
        PROPERTIES IMPORTED_LOCATION
        ${distribution_DIR}/ffmpeg/libs/libavdevice-57.so )

add_library( avfilter-6
        SHARED
        IMPORTED)
set_target_properties( avfilter-6
        PROPERTIES IMPORTED_LOCATION
        ${distribution_DIR}/ffmpeg/libs/libavfilter-6.so )

add_library( avformat-57
        SHARED
        IMPORTED)
set_target_properties( avformat-57
        PROPERTIES IMPORTED_LOCATION
        ${distribution_DIR}/ffmpeg/libs/libavformat-57.so )


add_library( avutil-55
        SHARED
        IMPORTED )
set_target_properties( avutil-55
        PROPERTIES IMPORTED_LOCATION
        ${distribution_DIR}/ffmpeg/libs/libavutil-55.so )

add_library( postproc-54
        SHARED
        IMPORTED )
set_target_properties( postproc-54
        PROPERTIES IMPORTED_LOCATION
        ${distribution_DIR}/ffmpeg/libs/libpostproc-54.so )

add_library( swresample-2
        SHARED
        IMPORTED )
set_target_properties( swresample-2
        PROPERTIES IMPORTED_LOCATION
        ${distribution_DIR}/ffmpeg/libs/libswresample-2.so )


add_library( swscale-4
        SHARED
        IMPORTED)
set_target_properties( swscale-4
        PROPERTIES IMPORTED_LOCATION
        ${distribution_DIR}/ffmpeg/libs/libswscale-4.so )

add_library( yuv
        SHARED
        IMPORTED)
set_target_properties( yuv
        PROPERTIES IMPORTED_LOCATION
        ${distribution_DIR}/ffmpeg/libs/libyuv.so )
#加载faac库
add_library( faac
        SHARED
        IMPORTED)
set_target_properties( faac
        PROPERTIES IMPORTED_LOCATION
        ${distribution_DIR}/faac/libs/libfaac.a )
#加载Rtmp库
add_library( rtmp
        SHARED
        IMPORTED)
set_target_properties( rtmp
        PROPERTIES IMPORTED_LOCATION
        ${distribution_DIR}/librtmp/libs/librtmp.a)
#加载X264库
add_library( x264
        SHARED
        IMPORTED)
set_target_properties( x264
        PROPERTIES IMPORTED_LOCATION
        ${distribution_DIR}/x264/libs/libx264.a )


#加载自己写的库
add_library( zqledia
        SHARED
        ${CMAKE_SOURCE_DIR}/src/main/cpp/media/ZQLMedia.cpp)

#find_library( log-lib
#              log )

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=gnu++11")

#
target_link_libraries(
        zqledia
        avcodec-57
        avdevice-57
        avfilter-6
        avformat-57
        avutil-55
        postproc-54
        swresample-2
        swscale-4
        faac
        rtmp
        x264
        OpenSLES
        yuv
        #系统库
        log
        android
)

