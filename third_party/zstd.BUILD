load("@rules_foreign_cc//foreign_cc:defs.bzl", "cmake")

package(default_visibility = ["//visibility:public"])

filegroup(
    name = "all_srcs",
    srcs = glob(["**"]),
)

cmake(
    name = "zstd",
    build_args = [
        "-j `nproc`",
    ],
    cache_entries = {
        "ZSTD_BUILD_TESTS": "OFF",
        "ZSTD_LEGACY_SUPPORT": "OFF",
    },
    lib_source = ":all_srcs",
    out_lib_dir = select({
        "@platforms//os:linux": "lib",
        "//conditions:default": "lib",
    }),
    out_shared_libs = select({
        "@platforms//os:macos": [
            "libzstd.dylib",
        ],
        "@platforms//os:linux": [
            "libzstd.so",
        ],
        "@platforms//os:windows": [
            "libzstd.dll",
        ],
    }),
    working_directory = "build/cmake",
)
