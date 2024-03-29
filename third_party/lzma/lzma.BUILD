# Description
#    lzma is a general purpose data compression library https://tukaani.org/xz/
#    Public Domain
#    Referenced https://github.com/nelhage/rules_boost/blob/master/BUILD.lzma

load("@bazel_skylib//rules:copy_file.bzl", "copy_file")

config_setting(
    name = "linux",
    constraint_values = ["@bazel_tools//platforms:linux"],
)

config_setting(
    name = "osx_arm64",
    constraint_values = [
        "@bazel_tools//platforms:osx",
        "@bazel_tools//platforms:aarch64",
    ],
)

config_setting(
    name = "osx_x86_64",
    constraint_values = [
        "@bazel_tools//platforms:osx",
        "@bazel_tools//platforms:x86_64",
    ],
)

config_setting(
    name = "windows",
    constraint_values = ["@bazel_tools//platforms:windows"],
)

config_setting(
    name = "android",
    constraint_values = ["@bazel_tools//platforms:android"],
)

copy_file(
    name = "copy_config",
    src = select({
        ":android": "@rules_compressor//third_party/lzma:config.lzma-linux.h",
        ":linux": "@rules_compressor//third_party/lzma:config.lzma-linux.h",
        ":osx_arm64": "@rules_compressor//third_party/lzma:config.lzma-osx-arm64.h",
        ":osx_x86_64": "@rules_compressor//third_party/lzma:config.lzma-osx-x86_64.h",
        ":windows": "@rules_compressor//third_party/lzma:config.lzma-windows.h",
    }),
    out = "src/liblzma/api/config.h",  # minimize the number of exported include paths
)

cc_library(
    name = "lzma",
    srcs = [
        "src/common/tuklib_cpucores.c",
        "src/common/tuklib_physmem.c",
        "src/liblzma/check/check.c",
        "src/liblzma/check/crc32_fast.c",
        "src/liblzma/check/crc32_table.c",
        "src/liblzma/check/crc64_fast.c",
        "src/liblzma/check/crc64_table.c",
        "src/liblzma/check/sha256.c",
        "src/liblzma/common/alone_decoder.c",
        "src/liblzma/common/alone_encoder.c",
        "src/liblzma/common/auto_decoder.c",
        "src/liblzma/common/block_buffer_decoder.c",
        "src/liblzma/common/block_buffer_encoder.c",
        "src/liblzma/common/block_decoder.c",
        "src/liblzma/common/block_encoder.c",
        "src/liblzma/common/block_header_decoder.c",
        "src/liblzma/common/block_header_encoder.c",
        "src/liblzma/common/block_util.c",
        "src/liblzma/common/common.c",
        "src/liblzma/common/easy_buffer_encoder.c",
        "src/liblzma/common/easy_decoder_memusage.c",
        "src/liblzma/common/easy_encoder.c",
        "src/liblzma/common/easy_encoder_memusage.c",
        "src/liblzma/common/easy_preset.c",
        "src/liblzma/common/filter_buffer_decoder.c",
        "src/liblzma/common/filter_buffer_encoder.c",
        "src/liblzma/common/filter_common.c",
        "src/liblzma/common/filter_decoder.c",
        "src/liblzma/common/filter_encoder.c",
        "src/liblzma/common/filter_flags_decoder.c",
        "src/liblzma/common/filter_flags_encoder.c",
        "src/liblzma/common/hardware_cputhreads.c",
        "src/liblzma/common/hardware_physmem.c",
        "src/liblzma/common/index.c",
        "src/liblzma/common/index_decoder.c",
        "src/liblzma/common/index_encoder.c",
        "src/liblzma/common/index_hash.c",
        "src/liblzma/common/outqueue.c",
        "src/liblzma/common/stream_buffer_decoder.c",
        "src/liblzma/common/stream_buffer_encoder.c",
        "src/liblzma/common/stream_decoder.c",
        "src/liblzma/common/stream_encoder.c",
        "src/liblzma/common/stream_encoder_mt.c",
        "src/liblzma/common/stream_flags_common.c",
        "src/liblzma/common/stream_flags_decoder.c",
        "src/liblzma/common/stream_flags_encoder.c",
        "src/liblzma/common/vli_decoder.c",
        "src/liblzma/common/vli_encoder.c",
        "src/liblzma/common/vli_size.c",
        "src/liblzma/delta/delta_common.c",
        "src/liblzma/delta/delta_decoder.c",
        "src/liblzma/delta/delta_encoder.c",
        "src/liblzma/lz/lz_decoder.c",
        "src/liblzma/lz/lz_encoder.c",
        "src/liblzma/lz/lz_encoder_mf.c",
        "src/liblzma/lzma/fastpos_table.c",
        "src/liblzma/lzma/lzma2_decoder.c",
        "src/liblzma/lzma/lzma2_encoder.c",
        "src/liblzma/lzma/lzma_decoder.c",
        "src/liblzma/lzma/lzma_encoder.c",
        "src/liblzma/lzma/lzma_encoder_optimum_fast.c",
        "src/liblzma/lzma/lzma_encoder_optimum_normal.c",
        "src/liblzma/lzma/lzma_encoder_presets.c",
        "src/liblzma/rangecoder/price_table.c",
        "src/liblzma/simple/arm.c",
        "src/liblzma/simple/armthumb.c",
        "src/liblzma/simple/ia64.c",
        "src/liblzma/simple/powerpc.c",
        "src/liblzma/simple/simple_coder.c",
        "src/liblzma/simple/simple_decoder.c",
        "src/liblzma/simple/simple_encoder.c",
        "src/liblzma/simple/sparc.c",
        "src/liblzma/simple/x86.c",
        "src/liblzma/api/config.h",
    ] + glob(["src/**/*.h"]),
    hdrs = [
        "src/liblzma/api/lzma.h",
        "src/liblzma/api/lzma/base.h",
        "src/liblzma/api/lzma/bcj.h",
        "src/liblzma/api/lzma/block.h",
        "src/liblzma/api/lzma/check.h",
        "src/liblzma/api/lzma/container.h",
        "src/liblzma/api/lzma/delta.h",
        "src/liblzma/api/lzma/filter.h",
        "src/liblzma/api/lzma/hardware.h",
        "src/liblzma/api/lzma/index.h",
        "src/liblzma/api/lzma/index_hash.h",
        "src/liblzma/api/lzma/lzma12.h",
        "src/liblzma/api/lzma/stream_flags.h",
        "src/liblzma/api/lzma/version.h",
        "src/liblzma/api/lzma/vli.h",
    ],
    copts = select({
        ":windows": [],
        "//conditions:default": ["-std=c99"],
    }) + [
        "-I external/org_lzma_lzma/src/common",
        "-I external/org_lzma_lzma/src/liblzma",
        "-I external/org_lzma_lzma/src/liblzma/api",
        "-I external/org_lzma_lzma/src/liblzma/common",
        "-I external/org_lzma_lzma/src/liblzma/check",
        "-I external/org_lzma_lzma/src/liblzma/delta",
        "-I external/org_lzma_lzma/src/liblzma/lz",
        "-I external/org_lzma_lzma/src/liblzma/lzma",
        "-I external/org_lzma_lzma/src/liblzma/rangecoder",
        "-I external/org_lzma_lzma/src/liblzma/simple",
    ],
    defines = select({
        ":windows": ["LZMA_API_STATIC"],
        "//conditions:default": [],
    }),
    includes = [
        "src/liblzma/api",
    ],
    linkopts = select({
        ":android": [],
        "//conditions:default": ["-lpthread"],
    }),
    linkstatic = select({
        ":windows": True,
        "//conditions:default": False,
    }),
    local_defines = [
        "HAVE_CONFIG_H",
    ],
    visibility = ["//visibility:public"],
)
