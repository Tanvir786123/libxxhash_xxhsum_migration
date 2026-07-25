load("@rules_cc//cc:defs.bzl", "cc_binary", "cc_library")
load("@bazel_skylib//lib:selects.bzl", "selects")

config_setting(
    name = "x86_64_platform",
    constraint_values = [
        "@platforms//cpu:x86_64",
    ],
)

config_setting(
    name = "dispatch_enabled",
    define_values = {
        "dispatch": "true",
    },
)

selects.config_setting_group(
    name = "use_dispatch",
    match_all = [
        ":x86_64_platform",
        ":dispatch_enabled",
    ],
)

cc_library(
    name = "xxhash",
    srcs = [
        "xxhash.c",
    ] + select({
        ":use_dispatch": [
            "xxh_x86dispatch.c",
        ],
        "//conditions:default": [],
    }),
    hdrs = [
        "xxhash.h",
    ] + select({
        ":use_dispatch": [
            "xxh_x86dispatch.h",
        ],
        "//conditions:default": [],
    }),
    local_defines = select({
        ":use_dispatch": [
            "XXHSUM_DISPATCH=1",
        ],
        "//conditions:default": [],
    }),
    visibility = ["//visibility:public"],
)

cc_binary(
    name = "xxhsum",
    srcs = [
        "cli/xxhsum.c",
        "cli/xsum_arch.c",
        "cli/xsum_os_specific.c",
        "cli/xsum_output.c",
        "cli/xsum_sanity_check.c",
        "cli/xsum_bench.c",
    ] + glob([
        "cli/*.h",
    ]) + select({
        ":use_dispatch": [
            "xxh_x86dispatch.c",
            "xxh_x86dispatch.h",
        ],
        "//conditions:default": [],
    }),
    local_defines = select({
        ":use_dispatch": [
            "XXHSUM_DISPATCH=1",
        ],
        "//conditions:default": [],
    }),
    deps = [
        ":xxhash",
    ],
    visibility = ["//visibility:public"],
)

cc_library(
    name = "cli_headers",
    hdrs = [
        "cli/xsum_arch.h",
        "cli/xsum_config.h",
        "cli/xsum_os_specific.h",
        "cli/xsum_output.h",
    ],
    textual_hdrs = [
        "cli/xsum_output.c",
        "cli/xsum_os_specific.c",
    ],
    visibility = ["//visibility:public"],
)
