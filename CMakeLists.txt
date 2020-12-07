cmake_minimum_required(VERSION 3.2)
project(usb-1.0 C)

set(CMAKE_C_STANDARD 11)

include_directories(libusb)
include_directories(Xcode)

add_library(${PROJECT_NAME} SHARED
        libusb/os/darwin_usb.c
        libusb/os/darwin_usb.h
        libusb/os/threads_posix.c
        libusb/os/threads_posix.h
        libusb/os/poll_posix.c
        libusb/os/poll_posix.h
        libusb/core.c
        libusb/descriptor.c
        libusb/hotplug.c
        libusb/hotplug.h
        libusb/io.c
        libusb/libusb.h
        libusb/libusbi.h
        libusb/strerror.c
        libusb/sync.c
        libusb/version.h
        libusb/version_nano.h
        Xcode/config.h)

target_link_libraries(${PROJECT_NAME} "-framework CoreFoundation -framework IOKit")

set_target_properties(${PROJECT_NAME} PROPERTIES
        FRAMEWORK TRUE
        FRAMEWORK_VERSION A
        MACOSX_FRAMEWORK_IDENTIFIER info.libusb
        PUBLIC_HEADER libusb/libusb.h
        XCODE_ATTRIBUTE_CODE_SIGN_IDENTITY "libusb community"
        )