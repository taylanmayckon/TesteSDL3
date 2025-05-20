# Tutorial para compilar o SDL3

Esse repositório é um tutorial de como compilar a biblioteca SDL3 no VS Code, utilizando o CMakeLists.

O código hello.c é um código de exemplo disponível no repositório oficial do SDL, que está sendo utilizado aqui para testar se a biblioteca está sendo compilada corretamente.

# Passo 1: Instalar o compilador da linguagem C
No VS Code deve ser instalada as extensões:
- C/C++
- C/C++ Compile Run
- C/++ Extension Pack
- CMake
- CMake Tools

Ao instalar as extensões, clique na extensão "C/C++ Compile Run" e acesse o link com as instruções necessárias para instalação do compilador que será utilizado ([Link direto para o Windows](https://github.com/danielpinto8zz6/c-cpp-compile-run/blob/HEAD/docs/COMPILER_SETUP.md#Windows)), lá será possível instalar o [TDM GCC](https://jmeubank.github.io/tdm-gcc/download/).

Verifique se a instalação ocorreu da maneira correta através do Prompt de Comando:
```sh
gcc --version
mingw32-make --version
```

Deverão ser retornadas mensagens sobre a versão atual tanto do GCC quanto do MINGW.


# Passo 2: Clonar o repositório do SDL
Na pasta do projeto, clone o repositório oficial do SDL para a pasta vendored:
```sh
git clone https://github.com/libsdl-org/SDL.git vendored/SDL
```
Outra opção, que talvez seja mais aconselhável, é copiar os arquivos do SDL manualmente para a pasta vendored\SDL, isso garante que futuramente não existirão problemas de incompatibilidade de versão, ou até problemas com o próprio Git por clonar um repositório dentro de outro repositório.

# Passo 3: Crie o arquivo CMakeLists.txt
Na documentação oficial da SDL, existe um exemplo de CMakeLists mínimo para compilar um projeto simples que utiliza a biblioteca, que é:
```cmake
cmake_minimum_required(VERSION 3.16)
project(hello)

# set the output directory for built objects.
# This makes sure that the dynamic library goes into the build directory automatically.
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/$<CONFIGURATION>")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/$<CONFIGURATION>")

# This assumes the SDL source is available in vendored/SDL
add_subdirectory(vendored/SDL EXCLUDE_FROM_ALL)

# Create your game executable target as usual
add_executable(hello WIN32 hello.c)

# Link to the actual SDL3 library.
target_link_libraries(hello PRIVATE SDL3::SDL3)
```
O CMakeLists.txt precisa ser modificado para se adequar ao projeto do qual se está desenvolvendo, já que o arquivo "main" desse exemplo é o "hello.c", então isso sempre vai variar de um projeto para o outro.


# Passo 4: Compile o código
Se você instalou corretamente as extensões do VS Code, deve ser possível compilar diretamente da IDE, com:
  1. Pressionar CTRL + SHIFT + P -> CMake: Select a Kit
  2. Selecionar o GCC MinGW
  3. Fazer o build

Uma maneira alternativa seria compilar por fora do VS Code, utilizando o Prompt de Comando, com os seguintes passos:
```sh
cmake -S . -B build -G "MinGW Makefiles"
cmake --build build
```

Para executar o projeto, basta executar:
```sh
cd build
hello.exe
```





