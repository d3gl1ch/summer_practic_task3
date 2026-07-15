# Подключаем папку с заголовками, чтобы компилятор видел hex_viewer.h и getopt.h
include_directories(include)

# Собираем библиотеку. Пока файлов исходников .c нет, CMake будет ругаться, 
# поэтому временно укажем только getopt.c, остальные добавим в следующих коммитах.
# Опция STATIC указывает собирать статическую библиотеку.
add_library(hex_lib STATIC
    src/getopt.c
)

# Позволяет автоматически транслировать пути к заголовкам при линковке
target_include_directories(hex_lib PUBLIC include)

# Отключаем предупреждения MSVC о небезопасных функциях (например, fopen)
if(MSVC)
    target_compile_options(hex_lib PRIVATE /wd4996 /wd5045)
endif()