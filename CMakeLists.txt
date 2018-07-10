cmake_minimum_required( VERSION 3.8 )

project( irecovery )

find_library( LIBCURL curl )
find_library( LIBUSB usb-1.0 HINTS /usr/local/lib )
find_library( LIBPLIST plist HINTS /usr/local/lib )

add_library( irecovery src/libirecovery.c )
target_link_libraries( irecovery z ${LIBUSB} ${LIBCURL} ${LIBPLIST} )
target_include_directories( irecovery 
    PUBLIC
        include 
    PRIVATE
        /usr/local/include/libusb-1.0 )

if( BUILD_EXE )
    add_executable( irecovery_exe tools/irecovery.c )
    target_link_libraries( irecovery_exe irecovery )
endif()
