cmake_minimum_required(VERSION 3.10)

project(kernel)

add_definitions(-D__KERNEL__)
add_definitions(-D__x86_64__)
add_definitions(-DCONFIG_DEBUG_LIST)
add_definitions(-DCONFIG_INET)
set(kernel_base "Set your own path for kernel code")

include_directories(${kernel_base}/include)
include_directories(${kernel_base}/arch/x86/include)

include(cmake/net.cmake)
include(cmake/kernel.cmake)
include(cmake/wg.cmake)
include(cmake/lib.cmake)
include(cmake/mm.cmake)
include(cmake/driver_base.cmake)
include(cmake/virtual_net_device.cmake)
add_library(kernel OBJECT
	${net_src}
	${core_src}
	${wg_src}
	${lib_src}
		${mm_src}
		${driver_base_src}
		${virtual_device_src}

)
