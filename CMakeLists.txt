cmake_minimum_required(VERSION 3.14)

project(MyZMQApp VERSION 0.1 LANGUAGES C)

set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)

find_package(PkgConfig REQUIRED)
pkg_check_modules(ZMQ REQUIRED libzmq)

include_directories(${ZMQ_INCLUDE_DIRS} include)

# Создание исполняемого файла для клиента
add_executable(MyZMQClient tests/client.c)
target_link_libraries(MyZMQClient ${ZMQ_LIBRARIES})

# Создание исполняемого файла для сервера
add_executable(MyZMQServer tests/server.c)
target_link_libraries(MyZMQServer ${ZMQ_LIBRARIES})

# Установка свойств для исполняемых файлов
set_target_properties(MyZMQClient PROPERTIES
    WIN32_EXECUTABLE ON
    MACOSX_BUNDLE OFF
)

set_target_properties(MyZMQServer PROPERTIES
    WIN32_EXECUTABLE ON
    MACOSX_BUNDLE OFF
)
