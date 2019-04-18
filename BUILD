load("@io_bazel_skydoc//stardoc:stardoc.bzl", "stardoc")
load("@bazel_skylib//:bzl_library.bzl", "bzl_library")

exports_files(["defs.bzl"])

licenses(["notice"]) # Apache 2.0

stardoc(
    name = "defs",
    input = "defs.bzl",
    out = "defs.md",
    deps = ["//:implementation"],
    symbol_names = ["maven_install"]
)

stardoc(
    name = "specs",
    input = "specs.bzl",
    out = "specs.md",
    deps = ["//:implementation"],
    symbol_names = ["maven.artifact", "maven.repository", "maven.exclusion"]
)

bzl_library(
    name = "implementation",
    srcs = [
        ":defs.bzl",
        ":specs.bzl",
        ":coursier.bzl",
        "//:private/versions.bzl",
        "//:private/special_artifacts.bzl",
        "//third_party/bazel_json/lib:json_parser.bzl"
    ],
)

genrule(
    name = "generate_api_reference",
    srcs = [
        "//:docs/includes/main_functions_header.md",
        "defs.md",
        "//:docs/includes/spec_functions_header.md",
        "specs.md",
    ],
    outs = ["api.md"],
    cmd = """cat \
    $(location //:docs/includes/main_functions_header.md) \
    $(location //:defs.md) \
    $(location //:docs/includes/spec_functions_header.md) \
    $(location //:specs.md) > $@""",
)
