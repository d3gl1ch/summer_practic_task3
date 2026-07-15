include_directories(include)

# Добавляем в список компилируемых файлов библиотеки hex_viewer.c
add_library(hex_lib STATIC
    src/getopt.c
    src/hex_viewer.c
)

target_include_directories(hex_lib PUBLIC include)

if(MSVC)
    target_compile_options(hex_lib PRIVATE /wd4996 /wd5045)
endif()