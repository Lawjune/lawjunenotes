# CMAKE TUTORIAL

## CMAKE TUTORIAL EP1 | Understanding The Basics

### Basic Concept of `makefile`
- It is just a file called a make-file and it runs commands so at the top it'll have like
	```sh
	default:
		g++ main.cpp -o out
	```

```cpp
#include <iostream>
int main(int argc, char* argv[]) 
{
    std::cout << "Hey, Zues!\n";

    return 0;
}
```

### CMAKE

So CMAKE relies on a top level file called `CMakeLists.txt`.

Create the `CMakeLists.txt` in the root directory of the project.
```sh
touch CMakeLists.txt
```
=> We can `rm` the `makefile` and `out` since we are using CMAKE.

Get from `cmake --help`
```sh
cmake [options] -S <path-to-source> -B <path-to-build>
```

Make the build folder
```sh
mkdir build
cd build
cmake -S ../ -B .
```

```sh
(base) lawjune@IC:~/Projects/OurLoardAndSavior/build$ ll
total 40
drwxr-xr-x 3 lawjune lawjune  4096 9月   6 10:00 ./
drwxr-xr-x 3 lawjune lawjune  4096 9月   6 10:00 ../
-rw-r--r-- 1 lawjune lawjune 13997 9月   6 10:00 CMakeCache.txt
drwxr-xr-x 4 lawjune lawjune  4096 9月   6 10:00 CMakeFiles/
-rw-r--r-- 1 lawjune lawjune  1656 9月   6 10:00 cmake_install.cmake
-rw-r--r-- 1 lawjune lawjune  4135 9月   6 10:00 Makefile
```

```sh
(base) lawjune@IC:~/Projects/OurLoardAndSavior$ cmake --version
cmake version 3.21.2

CMake suite maintained and supported by Kitware (kitware.com/cmake).
```

=> `CMakeFiles.txt`
- Set the CMAKE version
```c
cmake_minimum_required(VERSION 3.21.2)
```

- Set up the project
```c
project(OLAS)
```

- Configure executable file with `FILE_NAME` and `SOURCE`
```c
add_executable(${PROJECT_NAME} main.cpp)
```

=> Make target
```sh
(base) lawjune@IC:~/Projects/OurLoardAndSavior/build$ make
[ 50%] Building CXX object CMakeFiles/OLAS.dir/main.cpp.o
[100%] Linking CXX executable OLAS
[100%] Built target OLAS
(base) lawjune@IC:~/Projects/OurLoardAndSavior/build$ OLAS 
Hey, Zues!
```
***CMakeLists.txt of this EP***
```c
cmake_minimum_required(VERSION 3.21.2)

project(OLAS)

add_executable(${PROJECT_NAME} main.cpp)
```

## CMAKE TUTORIAL EP2 | Libraries and Subdirectories

### LEVELS

```sh
(base) lawjune@IC:~/Projects/OurLoardAndSavior$ touch adder.cpp
```

=>`adder.cpp`
```c
float add(float a, float b)
{
    return (a + b) ;
}
```

=> `main.cpp`
```c
#include <iostream>

float add(float a, float b);

int main(int argc, char* argv[]) 
{
    std::cout << "Hey, Zues!\n";

    std::cout << add(72.1f, 73.8f) << '\n';

    return 0;
}
```

=> `CMakeLists.txt`
Add the `adder.cpp` into the executable source
```c
cmake_minimum_required(VERSION 3.21.2)

project(OLAS)

add_executable(${PROJECT_NAME} main.cpp adder.cpp)
```

```sh
(base) lawjune@IC:~/Projects/OurLoardAndSavior$ cmake -S . -B build
-- Configuring done
-- Generating done
-- Build files have been written to: /home/lawjune/Projects/OurLoardAndSavior/build
(base) lawjune@IC:~/Projects/OurLoardAndSavior$ cd build/
(base) lawjune@IC:~/Projects/OurLoardAndSavior/build$ make
Consolidate compiler generated dependencies of target OLAS
[ 33%] Building CXX object CMakeFiles/OLAS.dir/adder.cpp.o
[ 66%] Linking CXX executable OLAS
[100%] Built target OLAS
(base) lawjune@IC:~/Projects/OurLoardAndSavior/build$ OLAS 
Hey, Zues!
145.9
```

### STATIC LIBS

*Note: Remove the `adder.cpp` from the add_executable.*

```sh
(base) lawjune@IC:~/Projects/OurLoardAndSavior/Adder$ ll
total 16
drwxrwxr-x 2 lawjune lawjune 4096 9月   6 10:24 ./
drwxr-xr-x 4 lawjune lawjune 4096 9月   6 10:23 ../
-rw-r--r-- 1 lawjune lawjune   52 9月   6 10:23 adder.cpp
-rw-rw-r-- 1 lawjune lawjune   28 9月   6 10:24 adder.h
```

=> `adder.h`
```c
float add(float a, float b);
```

=> `adder.c`
```c
#include "adder.h"

float add(float a, float b)
{
    return (a + b) ;
}
```

Make the *sub-level* of `CMakeLists.txt` in `Adder` folder.
```sh
(base) lawjune@IC:~/Projects/OurLoardAndSavior/Adder$ touch CMakeLists.txt
```

=> `CMakeLists.txt` on root directory
```c
add_subdirectory(Adder)
```
The *root-level* `CMakeLists.txt` will go to the `Adder` folder and find the *sub-level* `CMakeLists.txt`.

=> `CMakeLists.txt` on *sub-level*
```c
add_library(adder adder.cpp)
```

Build the link between the *project* and the *library*.
=> `CMakeLists.txt` on root directory
```c
target_link_library(${PROJECT_NAME} adder)
```

Build the link between the *root_directory* and the *library_directory*
```c
target_link_directories(${PROJECT_NAME} PRIVATE Adder/)
```

```c
#include <iostream>
#include <adder.h>

int main(int argc, char* argv[]) 
{
    std::cout << "Hey, Zues!\n";

    std::cout << add(72.1f, 73.8f) << '\n';

    return 0;
}
```

```sh
(base) lawjune@IC:~/Projects/OurLoardAndSavior$ cmake -S . -B build
-- Configuring done
-- Generating done
-- Build files have been written to: /home/lawjune/Projects/OurLoardAndSavior/build
(base) lawjune@IC:~/Projects/OurLoardAndSavior$ make -C build/
make: Entering directory '/home/lawjune/Projects/OurLoardAndSavior/build'
make[1]: Entering directory '/home/lawjune/Projects/OurLoardAndSavior/build'
make[2]: Entering directory '/home/lawjune/Projects/OurLoardAndSavior/build'
Consolidate compiler generated dependencies of target adder
make[2]: Leaving directory '/home/lawjune/Projects/OurLoardAndSavior/build'
[ 50%] Built target adder
make[2]: Entering directory '/home/lawjune/Projects/OurLoardAndSavior/build'
Consolidate compiler generated dependencies of target OLAS
make[2]: Leaving directory '/home/lawjune/Projects/OurLoardAndSavior/build'
make[2]: Entering directory '/home/lawjune/Projects/OurLoardAndSavior/build'
[ 75%] Building CXX object CMakeFiles/OLAS.dir/main.cpp.o
[100%] Linking CXX executable OLAS
make[2]: Leaving directory '/home/lawjune/Projects/OurLoardAndSavior/build'
[100%] Built target OLAS
make[1]: Leaving directory '/home/lawjune/Projects/OurLoardAndSavior/build'
make: Leaving directory '/home/lawjune/Projects/OurLoardAndSavior/build'
(base) lawjune@IC:~/Projects/OurLoardAndSavior$ ./build/OLAS 
Hey, Zues!
145.9
```

***Note***
`CMakeLists.txt` implictly executes with
```c
target_include_directories(${PROJECT_NAME} PUBLIC Adder/)
```

*Check more details in `make` file.

***CMakeLists.txt of this EP***
```c
cmake_minimum_required(VERSION 3.21.2)

project(OLAS)

add_executable(${PROJECT_NAME} main.cpp)

add_subdirectory(Adder)

target_include_directories(${PROJECT_NAME} PUBLIC Adder/)

target_link_directories(${PROJECT_NAME} PRIVATE Adder/)

target_link_libraries(${PROJECT_NAME} adder)
```

## CMAKE TUTORIAL EP3 | Git Submodules (adding glfw windowing library example)

### SUBMODULES

```sh
(base) lawjune@IC:~/Projects/OurLoardAndSavior$ git init
Initialized empty Git repository in /home/lawjune/Projects/OurLoardAndSavior/.git/
```

```sh
(base) lawjune@IC:~/Projects/OurLoardAndSavior$ touch .gitignore
```

=> Google `gitignore for c++`
https://github.com/github/gitignore/blob/master/C%2B%2B.gitignore


=> Google `gitignore for cmake`
https://raw.githubusercontent.com/github/gitignore/master/CMake.gitignore


=> Ignore the `build` folder
```txt
build

[Bb][Uu][Ii][Ll][Dd]/
```

```sh
git submodule add --githubUrl
```

```sh
git submodule add https://github.com/glfw/glfw.git external/glfw
```

```sh
git commit -am "add submodule glfw"
```

```sh
touch configure.sh build.sh run.sh 
chmod +x configure.sh build.sh run.sh  
```

```sh
#! /bin/sh ./configure.sh

cmake -S . -B build
```

```sh
#! /bin/sh ./build.sh

cd build ; make 
```

```sh
#! /bin/sh ./run.sh

cd build ; ./OLAS 
```

=>Ad the external submodule `glfw` into `CMakeLists.txt`
```c
add_subdirectory(external/glfw)
```

```sh
(base) lawjune@IC:~/Projects/OurLoardAndSavior$ ./configure.sh 
-- Looking for pthread.h
-- Looking for pthread.h - found
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Failed
-- Looking for pthread_create in pthreads
-- Looking for pthread_create in pthreads - not found
-- Looking for pthread_create in pthread
-- Looking for pthread_create in pthread - found
-- Found Threads: TRUE  
-- Found Doxygen: /usr/bin/doxygen (found version "1.8.13") found components: doxygen 
-- Using X11 for window creation
-- Found X11: /usr/include   
-- Looking for XOpenDisplay in /usr/lib/x86_64-linux-gnu/libX11.so;/usr/lib/x86_64-linux-gnu/libXext.so
-- Looking for XOpenDisplay in /usr/lib/x86_64-linux-gnu/libX11.so;/usr/lib/x86_64-linux-gnu/libXext.so - found
-- Looking for gethostbyname
-- Looking for gethostbyname - found
-- Looking for connect
-- Looking for connect - found
-- Looking for remove
-- Looking for remove - found
-- Looking for shmat
-- Looking for shmat - found
-- Looking for IceConnectionNumber in ICE
-- Looking for IceConnectionNumber in ICE - found
-- Configuring done
-- Generating done
-- Build files have been written to: /home/lawjune/Projects/OurLoardAndSavior/build
```

### OPTIONS

Check the `CMakeLists.txt` in *`external/glfw`*
```c
option(BUILD_SHARED_LIBS "Build shared libraries" OFF)
option(GLFW_BUILD_EXAMPLES "Build the GLFW example programs" ${GLFW_STANDALONE})
option(GLFW_BUILD_TESTS "Build the GLFW test programs" ${GLFW_STANDALONE})
option(GLFW_BUILD_DOCS "Build the GLFW documentation" ON)
option(GLFW_INSTALL "Generate installation target" ON)
option(GLFW_VULKAN_STATIC "Assume the Vulkan loader is linked with the application" OFF)
```

We can change them during the runtime or configuring time.

=> Add `D${options} ON/OFF` in *`./configure.sh`*
```sh
#! /bin/sh ./configure.sh

cmake DGLFW_BUILD_DOCS=OFF -S . -B build
```

Check the `glfw` library in build/external/src.

=> Add the `glfw` library into the `CMakeLists.txt` 
```c
target_include_directories(${PROJECT_NAME} PUBLIC Adder/ PUBLIC external/glfw/include)

target_link_directories(${PROJECT_NAME} PRIVATE Adder PRIVATE external/glfw/src)

target_link_libraries(${PROJECT_NAME} adder glfw)
```

```c
#include <iostream>
#include <adder.h>
#include <GLFW/glfw3.h>

int main(int argc, char* argv[]) 
{
    std::cout << "Hey, Zues!\n";

    std::cout << add(72.1f, 73.8f) << '\n';


    // Codes copied from the gear example
    GLFWwindow *window;

    if( !glfwInit() )
    {
        fprintf( stderr, "Failed to initialize GLFW\n" );
        exit( EXIT_FAILURE );
    }

    window = glfwCreateWindow( 300, 300, "Gears", NULL, NULL );
    if (!window)
    {
        fprintf( stderr, "Failed to open GLFW window\n" );
        glfwTerminate();
        exit( EXIT_FAILURE );
    }

    // Main loop
    while( !glfwWindowShouldClose(window) )
    {
        // Draw gears
        // draw();

        // Update animation
        // animate();

        // Swap buffers
        glfwSwapBuffers(window);
        glfwPollEvents();
    }

    // Terminate GLFW
    glfwTerminate();

    return 0;
}
```

### VARIABLES

***Note***
If you clone the project form github, it's not going to automatically check out the sub modules. 

Make `CMAKE` to automatically grab those repos when it gets cloned.

```sh
git submodule update --init --recursive
```

Or copy the following existing text before we include the submodules:
```c
#           DOWNLOAD ALL THE SUBMODULES
find_package(Git QUIET)
if(GIT_FOUND AND EXISTS "${PROJECT_SOURCE_DIR}/.git")
# Update submodules as needed
    option(GIT_SUBMODULE "Check submodules during build" ON)
    if(GIT_SUBMODULE)
        message(STATUS "Submodule update")
        execute_process(COMMAND ${GIT_EXECUTABLE} submodule update --init --recursive
                        WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
                        RESULT_VARIABLE GIT_SUBMOD_RESULT)
        if(NOT GIT_SUBMOD_RESULT EQUAL "0")
            message(FATAL_ERROR "git submodule update --init failed with ${GIT_SUBMOD_RESULT}, please checkout submodules")
        endif()
    endif()
endif()

#           CHECK ALL THE SUBMODULES
if(NOT EXISTS "${PROJECT_SOURCE_DIR}/external/glfw/CMakeLists.txt")
    message(FATAL_ERROR "The glfw submodules was not downloaded! GIT_SUBMODULE was turned off or failed. Please update submodules and try again.")
endif()
```

```sh
(base) lawjune@IC:~/Projects/OurLoardAndSavior$ git add .
(base) lawjune@IC:~/Projects/OurLoardAndSavior$ git commit -am "add submodule pull down"
[master 9f03a70] add submodule pull down
 10 files changed, 158 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 Adder/CMakeLists.txt
 create mode 100644 Adder/adder.cpp
 create mode 100644 Adder/adder.h
 create mode 100644 CMakeLists.txt
 create mode 100755 build.sh
 create mode 100755 configure.sh
 create mode 100644 main.cpp
 create mode 100644 readme.nd
 create mode 100755 run.sh
```

***The Final `CMakeLists.txt` of this EP***
```c
cmake_minimum_required(VERSION 3.21.2)

project(OLAS)

add_executable(${PROJECT_NAME} main.cpp)

add_subdirectory(Adder)

add_subdirectory(external/glfw)

#           DOWNLOAD ALL THE SUBMODULES
find_package(Git QUIET)
if(GIT_FOUND AND EXISTS "${PROJECT_SOURCE_DIR}/.git")
# Update submodules as needed
    option(GIT_SUBMODULE "Check submodules during build" ON)
    if(GIT_SUBMODULE)
        message(STATUS "Submodule update")
        execute_process(COMMAND ${GIT_EXECUTABLE} submodule update --init --recursive
                        WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
                        RESULT_VARIABLE GIT_SUBMOD_RESULT)
        if(NOT GIT_SUBMOD_RESULT EQUAL "0")
            message(FATAL_ERROR "git submodule update --init failed with ${GIT_SUBMOD_RESULT}, please checkout submodules")
        endif()
    endif()
endif()

#           CHECK ALL THE SUBMODULES
if(NOT EXISTS "${PROJECT_SOURCE_DIR}/external/glfw/CMakeLists.txt")
    message(FATAL_ERROR "The glfw submodules was not downloaded! GIT_SUBMODULE was turned off or failed. Please update submodules and try again.")
endif()

target_include_directories(${PROJECT_NAME} PUBLIC Adder/ PUBLIC external/glfw/include)

target_link_directories(${PROJECT_NAME} PRIVATE Adder PRIVATE external/glfw/src)

target_link_libraries(${PROJECT_NAME} adder glfw)
```

## CMake Tutorial EP 4 | Versioning Source Code

Add the `VERSION` in `CMakeLists.txt` before `add_executable(${PROJECT_NAME} main.cpp)`

```c
project(OLAS VERSION 1.0)

configure_file(OLASConfig.h.in OLASConfig.h)
```

Tell the CMAKE where we can find the `VERSION` after `add_executable(${PROJECT_NAME} main.cpp)`

```c
target_include_directories(${PROJECT_NAME} PUBLIC ${PROJECT_BINARY_DIR})
```

Here we are
```c
project(OLAS VERSION 1.0)

configure_file(OLASConfig.h.in OLASConfig.h)

add_executable(${PROJECT_NAME} main.cpp)

target_include_directories(${PROJECT_NAME} PUBLIC ${PROJECT_BINARY_DIR})
```

- Add `OLASConfig.h.in` file.
```c
// OLASConfig.h.in

#define OLAS_VERSION_MAJOR @OLAS_VERSION_MAJOR@
#define OLAS_VERSION_MINOR @OLAS_VERSION_MINOR@
```

- Add the header in main.cpp. 
```c
#include <iostream>
#include <adder.h>
#include <GLFW/glfw3.h>
#include <OLASConfig.h>

int main(int argc, char* argv[]) 
{
    std::cout << "Hey, Zues!\n";

    std::cout << add(72.1f, 73.8f) << '\n';

    std::cout << argv[0] << " Version " << OLAS_VERSION_MAJOR << "." << OLAS_VERSION_MINOR << '\n'; 
```

## CMake Tutorial EP 5 | Making Libs Optional

=> Add the `Adder` option in `CMakeLists.txt`
```c
# adder use logic
option(USE_ADDER "A simple library for adding 2 floats." ON)

if(USE_ADDER)
    add_subdirectory(Adder)

    target_include_directories(${PROJECT_NAME} PUBLIC Adder)

    target_link_directories(${PROJECT_NAME} PRIVATE Adder)

    target_link_libraries(${PROJECT_NAME} adder)

endif()
```

And remove the `adder` stuff from `glfw` part.
```c
target_include_directories(${PROJECT_NAME} PUBLIC external/glfw/include)

target_link_directories(${PROJECT_NAME} PRIVATE external/glfw/src)

target_link_libraries(${PROJECT_NAME} glfw)
```

......

***Final `CMakeLists.txt` of this EP***
```c
cmake_minimum_required(VERSION 3.21.2)

project(OLAS VERSION 1.0)


# adder use logic
option(USE_ADDER "A simple library for adding 2 floats." ON)

if(USE_ADDER)
    add_subdirectory(Adder)

    list(APPEND EXTRA_LIB_DIRS "Adder")
    list(APPEND EXTRA_INCLUDE_DIRS "Adder")
    list(APPEND EXTRA_LINKS adder)

endif()

# configure_file
configure_file(OLASConfig.h.in OLASConfig.h)

add_executable(${PROJECT_NAME} main.cpp)

target_include_directories(${PROJECT_NAME} PUBLIC ${PROJECT_BINARY_DIR})



add_subdirectory(external/glfw)

#           DOWNLOAD ALL THE SUBMODULES
find_package(Git QUIET)
if(GIT_FOUND AND EXISTS "${PROJECT_SOURCE_DIR}/.git")
# Update submodules as needed
    option(GIT_SUBMODULE "Check submodules during build" ON)
    if(GIT_SUBMODULE)
        message(STATUS "Submodule update")
        execute_process(COMMAND ${GIT_EXECUTABLE} submodule update --init --recursive
                        WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
                        RESULT_VARIABLE GIT_SUBMOD_RESULT)
        if(NOT GIT_SUBMOD_RESULT EQUAL "0")
            message(FATAL_ERROR "git submodule update --init failed with ${GIT_SUBMOD_RESULT}, please checkout submodules")
        endif()
    endif()
endif()

#           CHECK ALL THE SUBMODULES
if(NOT EXISTS "${PROJECT_SOURCE_DIR}/external/glfw/CMakeLists.txt")
    message(FATAL_ERROR "The glfw submodules was not downloaded! GIT_SUBMODULE was turned off or failed. Please update submodules and try again.")
endif()

target_include_directories(${PROJECT_NAME} 
    PUBLIC external/glfw/include
    ${EXTRA_INCLUDE_DIRS}
)

target_link_directories(${PROJECT_NAME} 
    PRIVATE external/glfw/src
    ${EXTRA_LIB_DIRS}
)

target_link_libraries(${PROJECT_NAME} 
    ${EXTRA_LINKS} 
    glfw
)
```

```c
// OLASConfig.h.in

#define OLAS_VERSION_MAJOR @OLAS_VERSION_MAJOR@
#define OLAS_VERSION_MINOR @OLAS_VERSION_MINOR@

#cmakedefine USE_ADDER
```

```c
#include <iostream>
#include <GLFW/glfw3.h>
#include <OLASConfig.h>
#ifdef USE_ADDER
    #include <adder.h>
#endif


int main(int argc, char* argv[]) 
{
    std::cout << "Hey, Zues!\n";

#ifdef USE_ADDER
    std::cout << "using Adder lib: " << add(72.1f, 73.8f) << '\n';
#else
    std::cout << "NOT using Adder lib: " << 72.1f + 73.8f << '\n';
#endif

    std::cout << argv[0] << " Version " << OLAS_VERSION_MAJOR << "." << OLAS_VERSION_MINOR << '\n'; 


    // Codes copied from the gear example
    GLFWwindow *window;

    if( !glfwInit() )
    {
        fprintf( stderr, "Failed to initialize GLFW\n" );
        exit( EXIT_FAILURE );
    }

    window = glfwCreateWindow( 300, 300, "Gears", NULL, NULL );
    if (!window)
    {
        fprintf( stderr, "Failed to open GLFW window\n" );
        glfwTerminate();
        exit( EXIT_FAILURE );
    }

    // Main loop
    while( !glfwWindowShouldClose(window) )
    {
        // Draw gears
        // draw();

        // Update animation
        // animate();

        // Swap buffers
        glfwSwapBuffers(window);
        glfwPollEvents();
    }

    // Terminate GLFW
    glfwTerminate();

    return 0;
}
```

```sh
#! /bin/sh ./configure.sh

cmake -DGLFW_BUILD_DOCS=OFF -DUSE_ADDER=ON -S . -B build
```

## CMake Tutorial EP 6 | Installing Your Software! (part 1/2 of install)

=> Add the `install` in `Adder` sub-level `CMakeLits.txt`
```c
add_library(adder adder.cpp)

install(TARGETS adder DESTINATION lib)
install(FILES adder.h DESTINATION include)
```

=> Add the `install` in the root-level `CMakeLists.txt`
```c
install(TARGETS ${PROJECT_NAME} DESTINATION bin)
install(FILES "${PROJECT_BINARY_DIR}/OLASConfig.h" DESTINATION include)
```

```sh
touch install.sh
chmod +x install.sh
```

```sh
#! /bin/sh ./install.sh

cd build ; make install
```

```sh
sudo ./install.sh
```

```sh
(base) lawjune@IC:/usr/local/bin$ ls -lrt
total 336
...
-rwxr-xr-x 1 root root 342448 9月   6 16:40 OLAS
```

```sh
(base) lawjune@IC:/usr/local/lib$ ll
total 500
drwxr-xr-x  6 root root    4096 9月   6 16:50 ./
drwxr-xr-x 10 root root    4096 8月   6  2019 ../
drwxr-xr-x  3 root root    4096 9月   3 15:37 cmake/
-rw-r--r--  1 root root    1402 9月   3 08:08 libadder.a
-rw-r--r--  1 root root  482638 9月   6 14:34 libglfw3.a
...
```

## CMake Tutorial EP 7 | Installing With CPack! (part 2/2 of install)

=> Add the `CPACK` on the buttom of root-level `CMakeLists.txt`
```c
include(InstallRequiredSystemLibraries)
set(CPACK_RESOURCE_FILE_LICENSE "${CMAKE_CURRENT_SOURCE_DIR}/License.txt")
set(CPACK_PACKAGE_VERSION_MAJOR "${Tutorial_VERSION_MAJOR}")
set(CPACK_PACKAGE_VERSION_MINOR "${Tutorial_VERSION_MINOR}")
include(CPack)
```

```sh
(base) lawjune@IC:~/Projects/OurLoardAndSavior/build$ sudo chown -R $(whoami) install_manifest.txt 
(base) lawjune@IC:~/Projects/OurLoardAndSavior/build$ sudo chown -R $(whoami) install_manifest.txt 
(base) lawjune@IC:~/Projects/OurLoardAndSavior/build$ ./OLAS--Linux.sh
```

## CMake Tutorial EP 8 | find_library(...) (part 1/2 of find lib)

```sh
apt search glu
sudo apt-get install aptitude
sudo aptitude get install libglew-dev
sudo aptitude install freeglut3-dev
```

=> Add the `find library` in the root-level `CMakeLists.txt`
```c
find_library(myglewlib glew NAMES glew2 GLEW GLEW2 DOC "glew library")
```
*Check the CMAKE version for the documentation.*
https://cmake.org/cmake/help/latest/command/find_library.html?highlight=find_library
```c
find_library (
          <VAR>
          name | NAMES name1 [name2 ...] [NAMES_PER_DIR]
          [HINTS [path | ENV var]... ]
          [PATHS [path | ENV var]... ]
          [PATH_SUFFIXES suffix1 [suffix2 ...]]
          [DOC "cache documentation string"]
          [NO_CACHE]
          [REQUIRED]
          [NO_DEFAULT_PATH]
          [NO_PACKAGE_ROOT_PATH]
          [NO_CMAKE_PATH]
          [NO_CMAKE_ENVIRONMENT_PATH]
          [NO_SYSTEM_ENVIRONMENT_PATH]
          [NO_CMAKE_SYSTEM_PATH]
          [CMAKE_FIND_ROOT_PATH_BOTH |
           ONLY_CMAKE_FIND_ROOT_PATH |
           NO_CMAKE_FIND_ROOT_PATH]
         )
```

- `myglewlib`: Customized defined library name.
- `glew`: `libglew.so`, `libglew.a`, etc. the libraries included `glew`.
- We can get awawy just that `find_library(myglewlib glew)` without covering the additional cases.

=> Add the `if-else` after then
```c
if (${myglewlib} STREQUAL myglewlib-NOTFOUND)
    message(FATAL_ERROR "no glew, sad day")
else()
    message(STATUS "glew found! as ${myglewlib}")
endif()
```

*"If nothing is found, the result will be **<VAR>-NOTFOUND**"*

***REMEMBER***
It stores the lib in cache and doesn't look anymore if the lib was found previously. 
So remove the `build` folder if needed.


=> Add `find glu and gl library` after then
```c

find_library(myglulib glu NAMES GLU DOC "glu library")
if (${myglulib} STREQUAL myglulib-NOTFOUND)
    message(FATAL_ERROR "no glu, sad day")
else()
    message(STATUS "glu found! as ${myglulib}")
endif()

find_library(mygllib gl NAMES GL DOC "gl library")
if (${mygllib} STREQUAL mygllib-NOTFOUND)
    message(FATAL_ERROR "no gl, sad day")
else()
    message(STATUS "gl found! as ${mygllib}")
endif()
```

=> Add the `found libraries` to the `target_link_libraries`
```c
target_link_libraries(${PROJECT_NAME} 
    ${EXTRA_LINKS} 
    glfw
    ${myglewlib} 
    ${myglulib} 
    ${mygllib}
)
```

=> Add `include libraries` to test the adding result.

```c
#include <GL/glew.h>
#include <GL/glut.h>
#include <GLFW/glfw3.h>
```
***Note that the <GLFW/glfw3.h> MUST be included after <GL/*>, because `glfw` also includes `GL`.***

```sh
(base) lawjune@IC:~/Projects/OurLoardAndSavior$ ./configure.sh 
-- The C compiler identification is GNU 7.4.0
-- The CXX compiler identification is GNU 7.4.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- glew found! as /usr/lib/x86_64-linux-gnu/libGLEW.so
-- glu found! as /usr/lib/x86_64-linux-gnu/libGLU.so
-- gl found! as /usr/lib/x86_64-linux-gnu/libGL.so
......
......
```

```sh
(base) lawjune@IC:~/Projects/OurLoardAndSavior$ ./build.sh 
......
......
[ 89%] Built target glfw
[ 94%] Building CXX object CMakeFiles/OLAS.dir/main.cpp.o
[100%] Linking CXX executable OLAS
[100%] Built target OLAS
```

***`CMakeLists.txt` at the end of this EP***
```c
cmake_minimum_required(VERSION 3.21.2)

project(OLAS VERSION 1.0)

# Find libraries
find_library(myglewlib glew NAMES glew2 GLEW GLEW2 DOC "glew library")
if (${myglewlib} STREQUAL myglewlib-NOTFOUND)
    message(FATAL_ERROR "no glew, sad day")
else()
    message(STATUS "glew found! as ${myglewlib}")
endif()

find_library(myglulib glu NAMES GLU DOC "glu library")
if (${myglulib} STREQUAL myglulib-NOTFOUND)
    message(FATAL_ERROR "no glu, sad day")
else()
    message(STATUS "glu found! as ${myglulib}")
endif()

find_library(mygllib gl NAMES GL DOC "gl library")
if (${mygllib} STREQUAL mygllib-NOTFOUND)
    message(FATAL_ERROR "no gl, sad day")
else()
    message(STATUS "gl found! as ${mygllib}")
endif()



# adder use logic
option(USE_ADDER "A simple library for adding 2 floats." ON)

if(USE_ADDER)
    add_subdirectory(Adder)

    list(APPEND EXTRA_LIB_DIRS "Adder")
    list(APPEND EXTRA_INCLUDE_DIRS "Adder")
    list(APPEND EXTRA_LINKS adder)

endif()

# configure_file
configure_file(OLASConfig.h.in OLASConfig.h)

add_executable(${PROJECT_NAME} main.cpp)

target_include_directories(${PROJECT_NAME} PUBLIC ${PROJECT_BINARY_DIR})



add_subdirectory(external/glfw)

#           DOWNLOAD ALL THE SUBMODULES
find_package(Git QUIET)
if(GIT_FOUND AND EXISTS "${PROJECT_SOURCE_DIR}/.git")
# Update submodules as needed
    option(GIT_SUBMODULE "Check submodules during build" ON)
    if(GIT_SUBMODULE)
        message(STATUS "Submodule update")
        execute_process(COMMAND ${GIT_EXECUTABLE} submodule update --init --recursive
                        WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
                        RESULT_VARIABLE GIT_SUBMOD_RESULT)
        if(NOT GIT_SUBMOD_RESULT EQUAL "0")
            message(FATAL_ERROR "git submodule update --init failed with ${GIT_SUBMOD_RESULT}, please checkout submodules")
        endif()
    endif()
endif()

#           CHECK ALL THE SUBMODULES
if(NOT EXISTS "${PROJECT_SOURCE_DIR}/external/glfw/CMakeLists.txt")
    message(FATAL_ERROR "The glfw submodules was not downloaded! GIT_SUBMODULE was turned off or failed. Please update submodules and try again.")
endif()

target_include_directories(${PROJECT_NAME} 
    PUBLIC external/glfw/include
    ${EXTRA_INCLUDE_DIRS}
)

target_link_directories(${PROJECT_NAME} 
    PRIVATE external/glfw/src
    ${EXTRA_LIB_DIRS}
)

target_link_libraries(${PROJECT_NAME} 
    ${EXTRA_LINKS} 
    glfw
    ${myglewlib} 
    ${myglulib} 
    ${mygllib}
)

install(TARGETS ${PROJECT_NAME} DESTINATION bin)
install(FILES "${PROJECT_BINARY_DIR}/OLASConfig.h" DESTINATION include)

include(InstallRequiredSystemLibraries)
set(CPACK_RESOURCE_FILE_LICENSE "${CMAKE_CURRENT_SOURCE_DIR}/License.txt")
set(CPACK_PACKAGE_VERSION_MAJOR "${Tutorial_VERSION_MAJOR}")
set(CPACK_PACKAGE_VERSION_MINOR "${Tutorial_VERSION_MINOR}")
include(CPack)
```

## CMake Tutorial EP 9 | find_package modules and config options (2/2 of find libs)

https://cmake.org/cmake/help/latest/module/FindGit.html?highlight=findgit

https://cmake.org/cmake/help/latest/command/find_package.html?highlight=find_package


=> Comment the `find_libraries` in the root-level of `CMakeLists.txt`

=> Add `find_package` after then
```c
find_package(GLEW CONFIG REQUIRED)
```
*Note that `CONFIG` only available for the `package` has `*-config.cmake` (such as `glew-config.cmake`) in the `*/build/cmake` folder.*

Search `config.cmake` in https://github.com/SDL-mirror/SDL.
The config.cmake.in implies it wil be put in the build dir if you build SDL.

***`CMakeLists.txt` at the end of this EP***
```c
cmake_minimum_required(VERSION 3.21.2)

project(OLAS VERSION 1.0)

find_package(GLEW REQUIRED)

# adder use logic
option(USE_ADDER "A simple library for adding 2 floats." ON)

if(USE_ADDER)
    add_subdirectory(Adder)

    list(APPEND EXTRA_LIB_DIRS "Adder")
    list(APPEND EXTRA_INCLUDE_DIRS "Adder")
    list(APPEND EXTRA_LINKS adder)

endif()

add_executable(${PROJECT_NAME} main.cpp)

configure_file(OLASConfig.h.in OLASConfig.h)

target_include_directories(${PROJECT_NAME} PUBLIC ${PROJECT_BINARY_DIR})

#           DOWNLOAD ALL THE SUBMODULES
find_package(Git QUIET)
if(GIT_FOUND AND EXISTS "${PROJECT_SOURCE_DIR}/.git")
# Update submodules as needed
    option(GIT_SUBMODULE "Check submodules during build" ON)
    if(GIT_SUBMODULE)
        message(STATUS "Submodule update")
        execute_process(COMMAND ${GIT_EXECUTABLE} submodule update --init --recursive
                        WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
                        RESULT_VARIABLE GIT_SUBMOD_RESULT)
        if(NOT GIT_SUBMOD_RESULT EQUAL "0")
            message(FATAL_ERROR "git submodule update --init failed with ${GIT_SUBMOD_RESULT}, please checkout submodules")
        endif()
    endif()
endif()

#           CHECK ALL THE SUBMODULES
if(NOT EXISTS "${PROJECT_SOURCE_DIR}/external/glfw/CMakeLists.txt")
    message(FATAL_ERROR "The glfw submodules was not downloaded! GIT_SUBMODULE was turned off or failed. Please update submodules and try again.")
endif()

add_subdirectory(external/glfw)

target_include_directories(${PROJECT_NAME} 
    PUBLIC external/glfw/include
    ${EXTRA_INCLUDE_DIRS}
    ${GLEW_INCLUDE_DIRS}
)

target_link_directories(${PROJECT_NAME} 
    PUBLIC external/glfw/src
    ${EXTRA_LIB_DIRS}
)

target_link_libraries(${PROJECT_NAME} ${EXTRA_LINKS} glfw ${GLEW_LIBRARIES} GL GLU)

install(TARGETS ${PROJECT_NAME} DESTINATION bin)
install(FILES "${PROJECT_BINARY_DIR}/OLASConfig.h" DESTINATION include)

include(InstallRequiredSystemLibraries)
set(CPACK_RESOURCE_FILE_LICENSE "${CMAKE_CURRENT_SOURCE_DIR}/License.txt")
set(CPACK_PACKAGE_VERSION_MAJOR "${Tutorial_VERSION_MAJOR}")
set(CPACK_PACKAGE_VERSION_MINOR "${Tutorial_VERSION_MINOR}")
include(CPack)
```

***main.cpp at the end of this EP***
```c
#include <OLASConfig.h>
#include <GL/glew.h>
#include <GL/glu.h>
#include <GLFW/glfw3.h>
#ifdef USE_ADDER
#include <adder.h>
#endif
#include <iostream>
#include <string>

void PrintOpenGLErrors(char const *const Function, char const *const File, int const Line)
{
    bool Succeeded = true;

    GLenum Error = glGetError();
    if (Error != GL_NO_ERROR)
    {
        char const *ErrorString = (char const *)gluErrorString(Error);
        if (ErrorString)
            std::cerr << ("OpenGL Error in %s at line %d calling function %s: '%s'", File, Line, Function, ErrorString) << std::endl;
        else
            std::cerr << ("OpenGL Error in %s at line %d calling function %s: '%d 0x%X'", File, Line, Function, Error, Error) << std::endl;
    }
}

#ifdef _DEBUG
#define CheckedGLCall(x)                                         \
    do                                                           \
    {                                                            \
        PrintOpenGLErrors(">>BEFORE<< " #x, __FILE__, __LINE__); \
        (x);                                                     \
        PrintOpenGLErrors(#x, __FILE__, __LINE__);               \
    } while (0)
#define CheckedGLResult(x) \
    (x)                    \
        PrintOpenGLErrors(#x, __FILE__, __LINE__);
#define CheckExistingErrors(x) PrintOpenGLErrors(">>BEFORE<< " #x, __FILE__, __LINE__);
#else
#define CheckedGLCall(x) (x)
#define CheckedGLResult(x) (x)
#define CheckExistingErrors(x)
#endif

void PrintShaderInfoLog(GLint const Shader)
{
    int InfoLogLength = 0;
    int CharsWritten = 0;

    glGetShaderiv(Shader, GL_INFO_LOG_LENGTH, &InfoLogLength);

    if (InfoLogLength > 0)
    {
        GLchar *InfoLog = new GLchar[InfoLogLength];
        glGetShaderInfoLog(Shader, InfoLogLength, &CharsWritten, InfoLog);
        std::cout << "Shader Info Log:" << std::endl
                  << InfoLog << std::endl;
        delete[] InfoLog;
    }
}

int main(int argc, char** argv)
{
    std::cout << argv[0] << " Version " << OLAS_VERSION_MAJOR << "." << OLAS_VERSION_MINOR << '\n';

#ifdef USE_ADDER
    std::cout << "using Adder lib:" << add(72.1f, 73.8f) << '\n';
#else
    std::cout << "NOT USING Adder lib:" << 72.1f + 73.8f << '\n';
#endif

    GLFWwindow *window;

    if (!glfwInit())
        return -1;

    window = glfwCreateWindow(640, 480, "Hello, Zeus!", NULL, NULL);
    if (!window)
    {
        glfwTerminate();
        return -1;
    }
    glfwMakeContextCurrent(window);

    GLenum err = glewInit();
    if (GLEW_OK != err)
    {
        std::cerr << "Error: " << glewGetErrorString(err) << std::endl;
        glfwTerminate();
        return -1;
    }

    char const *VertexShaderSource = R"GLSL(
        #version 130
        in vec2 position;
        void main()
        {
            gl_Position = vec4(position, 0.0, 1.0);
        }
    )GLSL";

    char const *FragmentShaderSource = R"GLSL(
        #version 130
        out vec4 outColor;
        void main()
        {
            outColor = vec4(1.0, 1.0, 1.0, 1.0);
        }
    )GLSL";

    GLfloat const Vertices[] = {
        0.0f, 0.5f,
        0.5f, -0.5f,
        -0.5f, -0.5f};

    GLuint const Elements[] = {
        0, 1, 2};

    GLuint VAO;
    CheckedGLCall(glGenVertexArrays(1, &VAO));
    CheckedGLCall(glBindVertexArray(VAO));

    GLuint VBO;
    CheckedGLCall(glGenBuffers(1, &VBO));
    CheckedGLCall(glBindBuffer(GL_ARRAY_BUFFER, VBO));
    CheckedGLCall(glBufferData(GL_ARRAY_BUFFER, sizeof(Vertices), Vertices, GL_STATIC_DRAW));
    CheckedGLCall(glBindBuffer(GL_ARRAY_BUFFER, 0));

    GLuint EBO;
    CheckedGLCall(glGenBuffers(1, &EBO));
    CheckedGLCall(glBindBuffer(GL_ELEMENT_ARRAY_BUFFER, EBO));
    CheckedGLCall(glBufferData(GL_ELEMENT_ARRAY_BUFFER, sizeof(Elements), Elements, GL_STATIC_DRAW));

    GLint Compiled;

// #ifdef _DEBUG
    GLuint VertexShader = CheckedGLResult(glCreateShader(GL_VERTEX_SHADER));
// #else
//  GLuint VertexShader = glCreateShader(GL_VERTEX_SHADER);
// #endif

    CheckedGLCall(glShaderSource(VertexShader, 1, &VertexShaderSource, NULL));
    CheckedGLCall(glCompileShader(VertexShader));
    CheckedGLCall(glGetShaderiv(VertexShader, GL_COMPILE_STATUS, &Compiled));
    if (!Compiled)
    {
        std::cerr << "Failed to compile vertex shader!" << std::endl;
        PrintShaderInfoLog(VertexShader);
    }

    GLuint FragmentShader = CheckedGLResult(glCreateShader(GL_FRAGMENT_SHADER));
    // GLuint FragmentShader = glCreateShader(GL_FRAGMENT_SHADER);

    CheckedGLCall(glShaderSource(FragmentShader, 1, &FragmentShaderSource, NULL));
    CheckedGLCall(glCompileShader(FragmentShader));
    CheckedGLCall(glGetShaderiv(FragmentShader, GL_COMPILE_STATUS, &Compiled));
    if (!Compiled)
    {
        std::cerr << "Failed to compile fragment shader!" << std::endl;
        PrintShaderInfoLog(FragmentShader);
    }

    GLuint ShaderProgram = CheckedGLResult(glCreateProgram());

    // GLuint ShaderProgram = glCreateProgram();
    CheckedGLCall(glAttachShader(ShaderProgram, VertexShader));
    CheckedGLCall(glAttachShader(ShaderProgram, FragmentShader));
    CheckedGLCall(glBindFragDataLocation(ShaderProgram, 0, "outColor"));
    CheckedGLCall(glLinkProgram(ShaderProgram));
    CheckedGLCall(glUseProgram(ShaderProgram));

    GLint PositionAttribute = CheckedGLResult(glGetAttribLocation(ShaderProgram, "position"));
    // GLint PositionAttribute = glGetAttribLocation(ShaderProgram, "position");

    CheckedGLCall(glEnableVertexAttribArray(PositionAttribute));

    CheckedGLCall(glBindBuffer(GL_ARRAY_BUFFER, VBO));
    CheckedGLCall(glVertexAttribPointer(PositionAttribute, 2, GL_FLOAT, GL_FALSE, 0, 0));
    CheckedGLCall(glBindBuffer(GL_ARRAY_BUFFER, 0));

    while (!glfwWindowShouldClose(window))
    {
        CheckedGLCall(glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT));
        CheckedGLCall(glDrawElements(GL_TRIANGLES, 3, GL_UNSIGNED_INT, 0));

        glfwSwapBuffers(window);
        glfwPollEvents();
    }

    CheckedGLCall(glDeleteProgram(ShaderProgram));
    CheckedGLCall(glDeleteShader(FragmentShader));
    CheckedGLCall(glDeleteShader(VertexShader));

    CheckedGLCall(glDeleteBuffers(1, &EBO));
    CheckedGLCall(glDeleteBuffers(1, &VBO));
    CheckedGLCall(glDeleteVertexArrays(1, &VAO));

    glfwTerminate();
    return 0;
}
```

## CMake Tutorial EP 10 | Running CMake on Windows (like linux) (Over-explained)

## CMake Tutorial EP 11 | VSCODE | VCPKG Libraries | Project Setup Basics









