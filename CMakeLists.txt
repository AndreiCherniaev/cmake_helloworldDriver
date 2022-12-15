#see https://musteresel.github.io/posts/2020/02/cmake-template-linux-kernel-module.html

cmake_minimum_required(VERSION 3.0.0 FATAL_ERROR)

project(driver VERSION 0.1.0 LANGUAGES C)
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)


set(kerneldir "" CACHE STRING "Path to the kernel build directory")
if("${kerneldir}" STREQUAL "")
  execute_process(COMMAND uname -r OUTPUT_VARIABLE uname_r
                  OUTPUT_STRIP_TRAILING_WHITESPACE)
  set(kerneldir "/lib/modules/${uname_r}/build")
endif()
find_file(kernel_makefile NAMES Makefile
                          PATHS ${kerneldir} NO_DEFAULT_PATH)
if(NOT kernel_makefile)
  message(FATAL_ERROR "There is no Makefile in kerneldir!")
endif()




message("my kerneldir path is \"${kerneldir}\"")


# Find kernel headers
#list(APPEND CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake")
# find_package(KernelHeaders REQUIRED)
include_directories(${kerneldir})

set(DRIVER_FILE hello.ko)
#set(KBUILD_CMD $(MAKE) -C ${kerneldir} M=${CMAKE_CURRENT_BINARY_DIR} modules src=${CMAKE_CURRENT_SOURCE_DIR})
# set(module_cmd ${CMAKE_MAKE_PROGRAM} -C ${kerneldir} M=${CMAKE_CURRENT_BINARY_DIR})
# message("KBUILD_CMD  is \"${KBUILD_CMD}\"")

# Generate the Kbuild file through cmake.
FILE(WRITE ${CMAKE_CURRENT_SOURCE_DIR}/Kbuild "obj-m := hello.o")

add_custom_command(OUTPUT ${DRIVER_FILE}
        COMMAND ${KBUILD_CMD}
        WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
        DEPENDS hello.c VERBATIM)

add_custom_target(driver ALL DEPENDS ${DRIVER_FILE})



