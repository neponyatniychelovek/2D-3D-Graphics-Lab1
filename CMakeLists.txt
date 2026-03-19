cmake_minimum_required(VERSION 3.10)

project(PhotoEditor)

# Настройка путей
set(OpenCV_DIR "${CMAKE_SOURCE_DIR}/opencv/build/x64/vc16/lib")

find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})

# Создаем программу
add_executable(PhotoEditor main.cpp)
target_link_libraries(PhotoEditor ${OpenCV_LIBS})

# --- КОМАНДЫ КОПИРОВАНИЯ ---
# Копируем DLL
add_custom_command(TARGET PhotoEditor POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
    "${CMAKE_SOURCE_DIR}/opencv/build/x64/vc16/bin/opencv_world4120d.dll"
    $<TARGET_FILE_DIR:PhotoEditor>
)

# Копируем картинку
add_custom_command(TARGET PhotoEditor POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
    "${CMAKE_SOURCE_DIR}/mad.jpeg"
    $<TARGET_FILE_DIR:PhotoEditor>
)