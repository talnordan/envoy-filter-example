licenses(["notice"])  # Apache 2


load(
    "//bazel:envoy_build_system.bzl",
    "envoy_cc_binary",
    "envoy_cc_library",
    "envoy_cc_test",
, "envoy_package")

envoy_package()

envoy_cc_binary(
    name = "envoy",
    repository = "@envoy",
    deps = [
        ":echo2_config",
        "//source/exe:envoy_main_entry_lib",
    ],
)

envoy_cc_library(
    name = "echo2_lib",
    srcs = ["echo2.cc"],
    hdrs = ["echo2.h"],
    repository = "@envoy",
    deps = [
        "//include/envoy/buffer:buffer_interface",
        "//include/envoy/network:connection_interface",
        "//include/envoy/network:filter_interface",
        "//source/common/common:assert_lib",
        "//source/common/common:logger_lib",
    ],
)

envoy_cc_library(
    name = "echo2_config",
    srcs = ["echo2_config.cc"],
    repository = "@envoy",
    deps = [
        ":echo2_lib",
        "//include/envoy/network:filter_interface",
        "//include/envoy/registry:registry",
        "//include/envoy/server:filter_config_interface",
    ],
)

envoy_cc_test(
    name = "echo2_integration_test",
    srcs = ["echo2_integration_test.cc"],
    data =  ["echo2_server.yaml"],
    repository = "@envoy",
    deps = [
        ":echo2_config",
        "//test/integration:integration_lib"
    ],
)

sh_test(
    name = "envoy_binary_test",
    srcs = ["envoy_binary_test.sh"],
    data = [":envoy"],
)
