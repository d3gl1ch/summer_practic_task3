# Минимальная поддерживаемая версия CMake
cmake_minimum_required(VERSION 3.15)
# Имя проекта и язык программирования
project(HexViewer C)

# Установка стандарта C11
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)

# Включаем встроенное тестирование CTest
enable_testing()

# Подключаем папку cmake, чтобы CMake видел наш MyFunctions.cmake
list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")
include(MyFunctions)

# Создаем глобальную цель для запуска тестов
if(NOT TARGET test_all)
    add_custom_target(test_all
        COMMAND ${CMAKE_CTEST_COMMAND} -C $<CONFIG> --output-on-failure
        COMMENT "Running all test suites..."
    )
endif()

# Настройки для компилятора MSVC (Windows)
if(MSVC)
    set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreadedDLL")
endif()

# Подключаем папки с кодом библиотеки и приложения
add_subdirectory(lib)
add_subdirectory(app)