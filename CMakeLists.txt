cmake_minimum_required(VERSION 3.10)
project(JITEjecuter)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Directorio de includes apuntando a SRC/runtime
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/SRC/runtime)

# Archivos fuente del runtime y JIT dentro de SRC/
set(SOURCES
    SRC/runtime/main.cpp
    SRC/runtime/cpu_state.cpp
    SRC/runtime/elf/elf_loader.cpp
    SRC/runtime/jit/arm_decoder.cpp
    SRC/runtime/jit/thumb_decoder.cpp
    SRC/runtime/jit/x64_codegen.cpp
    SRC/runtime/jit/block_cache.cpp
    SRC/runtime/abi/imports.cpp
)

# Definir el ejecutable principal del JIT
add_executable(JITEjecuter ${SOURCES})

# Opcional: También podemos armar un ejecutable para el analizador ELF si querés
add_executable(TAElfAnalyzer SRC/ta_elf_analyzer.cpp SRC/runtime/elf/elf_loader.cpp)

# Guardar los binarios generados en la carpeta COMPILE
set_target_properties(JITEjecuter PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/COMPILE"
)

set_target_properties(TAElfAnalyzer PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/COMPILE"
)