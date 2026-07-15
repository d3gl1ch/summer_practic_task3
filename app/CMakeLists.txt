# Подключаем папки с заголовками нашей библиотеки
include_directories(../lib/include)

# Создаем исполняемый файл из main.c
add_executable(hex_prog src/main.c)

# Связываем исполняемый файл с нашей статической библиотекой hex_lib
target_link_libraries(hex_prog PRIVATE hex_lib)

# Отключаем предупреждения компилятора MSVC для исполняемого файла
if(MSVC)
    target_compile_options(hex_prog PRIVATE /wd4996 /wd5045)
endif()