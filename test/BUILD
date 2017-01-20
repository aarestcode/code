package(default_visibility = ["//visibility:public"])

cc_library(
    name = "test_lib",
    srcs = glob(["Src/*.cpp"]),
    # deps = [
    #     "//platform/comms:comms_bsp",
    # ]
)

cc_binary(
    name="test",
    srcs = ["Src/main.cpp"],
    deps =  [
             ":test_lib",
             ],
)
