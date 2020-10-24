CMAKE_MINIMUM_REQUIRED(VERSION 3.13)
PROJECT(ble_mqtt)
SET(CMAKE_CXX_STANDARD 11)

FIND_PACKAGE(PkgConfig REQUIRED)
PKG_CHECK_MODULES(GLIB REQUIRED glib-2.0)
PKG_CHECK_MODULES(GIO REQUIRED gio-2.0)
PKG_CHECK_MODULES(GOBJECT REQUIRED gobject-2.0)
FIND_PACKAGE(Threads REQUIRED)

INCLUDE_DIRECTORIES(include ${GLIB_INCLUDE_DIRS})

ADD_LIBRARY(ggk STATIC
        src/DBusInterface.cpp
        src/DBusMethod.cpp
        src/DBusObject.cpp
        src/Gobbledegook.cpp
        src/GattCharacteristic.cpp
        src/GattDescriptor.cpp
        src/GattInterface.cpp
        src/GattProperty.cpp
        src/GattService.cpp
        src/HciAdapter.cpp
        src/HciSocket.cpp
        src/Init.cpp
        src/Logger.cpp
        src/Mgmt.cpp
        src/Server.cpp
        src/ServerUtils.cpp
        src/Utils.cpp)

ADD_EXECUTABLE(standalone src/standalone.cpp)

TARGET_LINK_LIBRARIES(standalone LINK_PUBLIC ggk Threads::Threads
        ${GLIB_LIBRARIES} ${GIO_LIBRARIES} ${GOBJECT_LIBRARIES})
