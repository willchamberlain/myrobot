set(CMAKE_VERBOSE_MAKEFILE ON)

# Sets the minimum version of CMake required to build the native
# library. You should either keep the default value or only pass a
# value of 3.4.0 or lower.

cmake_minimum_required(VERSION 3.4.1)

MESSAGE( STATUS "CMAKE_SOURCE_DIR is: " ${CMAKE_SOURCE_DIR} )

# Import the prebuilt, static library libopencv_core.a
# The IMPORTED_LOCATION failed to correctly find the lib unless an absolute path was provided
#
add_library( opencv_core
             STATIC
             IMPORTED )
set_target_properties( # Specifies the target library.
                       opencv_core
                       PROPERTIES IMPORTED_LOCATION
                       ${CMAKE_SOURCE_DIR}/src/main/jniLibs/${ANDROID_ABI}/libopencv_core.a )

# Import the prebuilt, static library libopencv_highgui.a
# The IMPORTED_LOCATION failed to correctly find the lib unless an absolute path was provided
#
add_library( opencv_highgui
             STATIC
             IMPORTED )
set_target_properties( # Specifies the target library.
                       opencv_highgui
                       PROPERTIES IMPORTED_LOCATION
                       ${CMAKE_SOURCE_DIR}/src/main/jniLibs/${ANDROID_ABI}/libopencv_highgui.a )


# Import the prebuilt, static library libopencv_imgproc.a
# The IMPORTED_LOCATION failed to correctly find the lib unless an absolute path was provided
#
add_library( opencv_imgproc
             STATIC
             IMPORTED )
set_target_properties( # Specifies the target library.
                       opencv_imgproc
                       PROPERTIES IMPORTED_LOCATION
                       ${CMAKE_SOURCE_DIR}/src/main/jniLibs/${ANDROID_ABI}/libopencv_imgproc.a )

# Import the prebuilt, static library libopencv_java3.so
# The IMPORTED_LOCATION failed to correctly find the lib unless an absolute path was provided
#
add_library( opencv_java3
             SHARED
             IMPORTED )
set_target_properties( # Specifies the target library.
                       opencv_java3
                       PROPERTIES IMPORTED_LOCATION
                       ${CMAKE_SOURCE_DIR}/src/main/jniLibs/${ANDROID_ABI}/libopencv_java3.so )

# Import the prebuilt, static library libopencv_ml.a
# The IMPORTED_LOCATION failed to correctly find the lib unless an absolute path was provided
#
add_library( opencv_ml
             STATIC
             IMPORTED )
set_target_properties( # Specifies the target library.
                       opencv_ml
                       PROPERTIES IMPORTED_LOCATION
                       ${CMAKE_SOURCE_DIR}/src/main/jniLibs/${ANDROID_ABI}/libopencv_ml.a )

# Include the OpenCV native code
include_directories( /mnt/nixbig/downloads/OpenCV-android-sdk-3.4.1/OpenCV-android-sdk/sdk/native/jni/include )



# Import the prebuilt, static library libopencv_ts.a
# The IMPORTED_LOCATION failed to correctly find the lib unless an absolute path was provided
#
# add_library( opencv_ts
#              STATIC
#              IMPORTED )
# set_target_properties( # Specifies the target library.
#                        opencv_ts
#                        PROPERTIES IMPORTED_LOCATION
#                        ${CMAKE_SOURCE_DIR}/src/main/jniLibs/${ANDROID_ABI}/libopencv_ts.a )


 # Specifies a path to native header files.
 include_directories(src/main/jni/)

# Creates and names a library, sets it as either STATIC
# or SHARED, and provides the relative paths to its source code.
# You can define multiple libraries, and CMake builds it for you.
# Gradle automatically packages shared libraries with your APK.

add_library( # Sets the name of the library.
             myrobot

             # Sets the library as a shared library.
             SHARED

             # Provides a relative path to your source file(s).
             # Associated headers in the same location as their source
             # file are automatically included.
             src/main/jni/ball_detect.cpp
             src/main/jni/native.cpp
             )



# Searches for a specified prebuilt library and stores the path as a
# variable. Because system libraries are included in the search path by
# default, you only need to specify the name of the public NDK library
# you want to add. CMake verifies that the library exists before
# completing its build.

find_library( # Sets the name of the path variable.
              log-lib

              # Specifies the name of the NDK library that
              # you want CMake to locate.
              log )

find_library ( ANDROID_LIB
               android )
find_library ( EGL_LIB
               EGL )
find_library ( GLESV2_LIB
               GLESv2 )
find_library ( DL_LIB
               dl )
find_library ( Z_LIB
               z )

# Specifies libraries CMake should link to your target library. You
# can link multiple libraries, such as libraries you define in the
# build script, prebuilt third-party libraries, or system libraries.

target_link_libraries( # Specifies the target library.
                       myrobot
                       ${ANDROID_LIB}
                       ${EGL_LIB}
                       ${GLESV2_LIB}
                       ${DL_LIB}
                       ${Z_LIB}
                       opencv_core
                       opencv_highgui
                       opencv_imgproc
                       opencv_java3
                       opencv_ml
                       # opencv_ts
                       ${log-lib} )
