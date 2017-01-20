# This is the entry point for --crosstool_top.  Toolchains are found
# by lopping off the name of --crosstool_top and searching for
# 'cc-compiler-${CPU}' in this BUILD file, where CPU is the target CPU
# specified in --cpu.
#
# This file group should include
#   * all cc_toolchain targets supported
#   * all file groups that said cc_toolchain might refer to,
# including the default_grte_top setting in the CROSSTOOL
# protobuf.
#
#  crosscompile from a linux host to an arm target:
#
#   bazel build --host_cpu=k9 --crosstool_top=//tools/arm_compiler:toolchain --cpu=zynq_linux --verbose_failures test/cross_compile_for_arm/hello
#
#  k9 is the cpu designation for arbitrary linux x86 hosts it seems
package(default_visibility = ["//visibility:public"])

filegroup(
    name = "toolchain_fg",
    srcs = [
        ":cc-compiler-sama5d3xek",  # crosscompile for sama5d3xek
        ":cc-compiler-k9",          # linux host
        ":linaro_linux_all_files",
        "@org_linaro_components_toolchain_gcc_5_3_1//:compiler_components",
    ],
)

filegroup(
    name = "srcs",
    srcs = glob(["**"]) + [
        "//tools/arm_compiler/linaro_linux_gcc:srcs",
    ],
    visibility = ["//visibility:public"],
)

cc_toolchain_suite(
    name = "toolchain",
    # target_cpu | compiler
    toolchains = {
        "sama5d3xek|gcc": "cc-compiler-sama5d3xek", # crosscompile for sama5d3xek
        "k9|compiler": "cc-compiler-k9",            # linux host
    },
)

filegroup(
    name = "linaro_linux_all_files",
    srcs = [
        "//tools/arm_compiler/linaro_linux_gcc:tool-wrappers",
        "@org_linaro_components_toolchain_gcc_5_3_1//:compiler_pieces",
    ],
)

filegroup(
    name = "linaro_linux_linker_files",
    srcs = [
        "//tools/arm_compiler/linaro_linux_gcc:ar",
        "//tools/arm_compiler/linaro_linux_gcc:gcc",
        "//tools/arm_compiler/linaro_linux_gcc:ld",
        "@org_linaro_components_toolchain_gcc_5_3_1//:compiler_pieces",
    ],
)

filegroup(
    name = "linaro_linux_compiler_files",
    srcs = [
        "//tools/arm_compiler/linaro_linux_gcc:as",
        "//tools/arm_compiler/linaro_linux_gcc:gcc",
        "//tools/arm_compiler/linaro_linux_gcc:ld",
    ],
)

filegroup(
    name = "empty",
    srcs = [],
)

cc_toolchain(
    name = "cc-compiler-sama5d3xek",
    all_files = ":linaro_linux_all_files",
    compiler_files = ":linaro_linux_compiler_files",
    cpu = "sama5d3xek",
    dwp_files = ":empty",
    dynamic_runtime_libs = [":empty"],
    linker_files = ":linaro_linux_linker_files",
    objcopy_files = "//tools/arm_compiler/linaro_linux_gcc:objcopy",
    static_runtime_libs = [":empty"],
    strip_files = "//tools/arm_compiler/linaro_linux_gcc:strip",
    supports_param_files = 1,
    visibility = ["//visibility:public"],
)

# the host already has all the files it needs
cc_toolchain(
    name = "cc-compiler-k9",
    all_files = ":empty",
    compiler_files = ":empty",
    cpu = "local",
    dwp_files = ":empty",
    dynamic_runtime_libs = [":empty"],
    linker_files = ":empty",
    objcopy_files = ":empty",
    static_runtime_libs = [":empty"],
    strip_files = ":empty",
    supports_param_files = 1,
)
