cmake_minimum_required(VERSION 3.10)

project(kernel)

add_definitions(-D__KERNEL__)
add_definitions(-D__x86_64__)
add_definitions(-DCONFIG_DEBUG_LIST)
add_definitions(-DCONFIG_INET)
add_definitions(-DCONFIG_SECURITY_NETWORK)

add_definitions(-DCONFIG_NET_CLS_ACT)
add_definitions(-DCONFIG_NET_EGRESS)
add_definitions(-DCONFIG_NET_CLS)
add_definitions(-DCONFIG_BPF_EVENTS)
add_definitions(-DCONFIG_PERF_EVENTS)
add_definitions(-DCONFIG_BPF_SYSCALL)
add_definitions(-DCONFIG_EVENT_TRACING)
add_definitions(-DCONFIG_CGROUP_PERF)
add_definitions(-DCONFIG_SECURITY)
add_definitions(-DCONFIG_BPF_JIT)
add_definitions(-DCONFIG_HAVE_EBPF_JIT)
add_definitions(-DCONFIG_KALLSYMS)
add_definitions(-DCONFIG_MODULES)
add_definitions(-DCONFIG_SYSCTL)
add_definitions(-DCONFIG_PROC_SYSCTL)
add_definitions(-DCONFIG_AUDITSYSCALL)
add_definitions(-DCONFIG_PROC_FS)
add_definitions(-DCONFIG_BPF)
add_definitions(-DCONFIG_CGROUP_BPF)
add_definitions(-DCONFIG_CGROUPS)
add_definitions(-DCONFIG_SOCK_CGROUP_DATA)
add_definitions(-DCONFIG_NET)
add_definitions(-DCONFIG_X86_32)
add_definitions(-DCONFIG_X86_64)

set(kernel_base ${CMAKE_CURRENT_SOURCE_DIR}/linux-4.19.248)

include_directories(${kernel_base}/include)
include_directories(${kernel_base}/arch/x86/include)

include(cmake/net.cmake)
include(cmake/kernel.cmake)
include(cmake/lib.cmake)
include(cmake/mm.cmake)
include(cmake/driver_base.cmake)
include(cmake/security.cmake)
include(cmake/fs.cmake)
include(cmake/arch.cmake)
add_library(kernel OBJECT
	${net_src}
	${core_src}
	${lib_src}
	${mm_src}
	${driver_base_src}
	${security_src}
	${fs_src}
	${arch_src}
)
