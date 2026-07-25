load("@rules_cc//cc:defs.bzl", "cc_test")
load("@rules_shell//shell:sh_test.bzl", "sh_test")

sh_test(
    name = "test_filename_escape",
    size = "small",
    srcs = [
        "filename-escape.sh",
    ],
    data = [
        "//:xxhsum",
    ],
)

cc_test(
    name = "test_sanity",
    size = "small",
    srcs = [
        "sanity_test.c",
        "sanity_test_vectors.h",
    ],
    deps = [
        "//:xxhash",
        "//:cli_headers",
    ],
)
