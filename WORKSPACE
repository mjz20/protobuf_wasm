workspace(name = "com_google_protobuf")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

local_repository(
    name = "com_google_protobuf_examples",
    path = "examples",
)

http_archive(
    name = "com_google_googletest",
    sha256 = "ea54c9845568cb31c03f2eddc7a40f7f83912d04ab977ff50ec33278119548dd",
    strip_prefix = "googletest-4c9a3bb62bf3ba1f1010bf96f9c8ed767b363774",
    urls = [
        "https://github.com/google/googletest/archive/4c9a3bb62bf3ba1f1010bf96f9c8ed767b363774.tar.gz",
    ],
)

http_archive(
    name = "com_googlesource_code_re2",
    sha256 = "906d0df8ff48f8d3a00a808827f009a840190f404559f649cb8e4d7143255ef9",
    strip_prefix = "re2-a276a8c738735a0fe45a6ee590fe2df69bcf4502",
    urls = ["https://github.com/google/re2/archive/a276a8c738735a0fe45a6ee590fe2df69bcf4502.zip"],  # 2022-04-08
)

# Bazel platform rules.
http_archive(
    name = "platforms",
    sha256 = "a879ea428c6d56ab0ec18224f976515948822451473a80d06c2e50af0bbe5121",
    strip_prefix = "platforms-da5541f26b7de1dc8e04c075c99df5351742a4a2",
    urls = ["https://github.com/bazelbuild/platforms/archive/da5541f26b7de1dc8e04c075c99df5351742a4a2.zip"],  # 2022-05-27
)

# Load common dependencies.
load("//:protobuf_deps.bzl", "PROTOBUF_MAVEN_ARTIFACTS", "protobuf_deps")
protobuf_deps()

load("@rules_jvm_external//:defs.bzl", "maven_install")

maven_install(
    artifacts = PROTOBUF_MAVEN_ARTIFACTS,
    # For updating instructions, see:
    # https://github.com/bazelbuild/rules_jvm_external#updating-maven_installjson
    maven_install_json = "//:maven_install.json",
    repositories = [
        "https://repo1.maven.org/maven2",
        "https://repo.maven.apache.org/maven2",
    ],
)

load("@maven//:defs.bzl", "pinned_maven_install")

pinned_maven_install()

# For `cc_proto_blacklist_test` and `build_test`.
load("@bazel_skylib//:workspace.bzl", "bazel_skylib_workspace")

bazel_skylib_workspace()

load("@rules_pkg//:deps.bzl", "rules_pkg_dependencies")
rules_pkg_dependencies()

# For `kt_jvm_library`
load("@io_bazel_rules_kotlin//kotlin:repositories.bzl", "kotlin_repositories")
kotlin_repositories()

load("@io_bazel_rules_kotlin//kotlin:core.bzl", "kt_register_toolchains")
kt_register_toolchains()

load("@upb//bazel:workspace_deps.bzl", "upb_deps")
upb_deps()

load("@upb//bazel:system_python.bzl", "system_python")
system_python(
    name = "system_python",
    minimum_python_version = "3.7",
)

load("@system_python//:pip.bzl", "pip_parse")
pip_parse(
    name="pip_deps",
    requirements = "@upb//python:requirements.txt",
    requirements_overrides = {
        "3.11": "@upb//python:requirements_311.txt",
    },
)

load("@pip_deps//:requirements.bzl", "install_deps")
install_deps()

load("@utf8_range//:workspace_deps.bzl", "utf8_range_deps")
utf8_range_deps()

bind(
    name = "python_headers",
    actual = "@system_python//:python_headers",
)


#add by mjz20
http_archive(
    name = "emsdk",
    sha256 = "b8270749b99d8d14922d1831b93781a5560fba6f7bce65cd477fc1b6aa262535",
    strip_prefix = "emsdk-3.1.28/bazel",
    url = "https://github.com/emscripten-core/emsdk/archive/refs/tags/3.1.28.tar.gz",
)

load("@emsdk//:deps.bzl", emsdk_deps = "deps")
emsdk_deps()

load("@emsdk//:emscripten_deps.bzl", emsdk_emscripten_deps = "emscripten_deps")
emsdk_emscripten_deps(emscripten_version = "3.1.28")

load("@emsdk//:toolchains.bzl", "register_emscripten_toolchains")
register_emscripten_toolchains()
#end