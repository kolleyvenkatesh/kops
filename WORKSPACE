load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")

#=============================================================================
# Go rules

http_archive(
    name = "io_bazel_rules_go",
    sha256 = "207fad3e6689135c5d8713e5a17ba9d1290238f47b9ba545b63d9303406209c6",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_go/releases/download/v0.24.7/rules_go-v0.24.7.tar.gz",
        "https://github.com/bazelbuild/rules_go/releases/download/v0.24.7/rules_go-v0.24.7.tar.gz",
    ],
)

http_archive(
    name = "bazel_gazelle",
    sha256 = "b85f48fa105c4403326e9525ad2b2cc437babaa6e15a3fc0b1dbab0ab064bc7c",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-gazelle/releases/download/v0.22.2/bazel-gazelle-v0.22.2.tar.gz",
        "https://github.com/bazelbuild/bazel-gazelle/releases/download/v0.22.2/bazel-gazelle-v0.22.2.tar.gz",
    ],
)

load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")

go_rules_dependencies()

go_register_toolchains(
    go_version = "1.15.5",
)

load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies", "go_repository")

gazelle_dependencies()

#=============================================================================
# Docker rules

http_archive(
    name = "io_bazel_rules_docker",
    sha256 = "4521794f0fba2e20f3bf15846ab5e01d5332e587e9ce81629c7f96c793bb7036",
    strip_prefix = "rules_docker-0.14.4",
    urls = ["https://github.com/bazelbuild/rules_docker/releases/download/v0.14.4/rules_docker-v0.14.4.tar.gz"],
)

load(
    "@io_bazel_rules_docker//repositories:repositories.bzl",
    container_repositories = "repositories",
)

container_repositories()

load("@io_bazel_rules_docker//repositories:deps.bzl", container_deps = "deps")

container_deps()

load("@io_bazel_rules_docker//repositories:pip_repositories.bzl", "pip_deps")

pip_deps()

load(
    "@io_bazel_rules_docker//repositories:go_repositories.bzl",
    docker_go_deps = "go_deps",
)

docker_go_deps()

load(
    "@io_bazel_rules_docker//container:container.bzl",
    "container_pull",
)

# TODO(fejta): use load.bzl, repos.bzl from repo-infra
git_repository(
    name = "io_k8s_repo_infra",
    commit = "db6ceb5f992254db76af7c25db2edc5469b5ea82",
    remote = "https://github.com/kubernetes/repo-infra.git",
    shallow_since = "1570128715 -0700",
)

http_archive(
    name = "bazel_toolchains",
    sha256 = "1342f84d4324987f63307eb6a5aac2dff6d27967860a129f5cd40f8f9b6fd7dd",
    strip_prefix = "bazel-toolchains-2.2.0",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-toolchains/releases/download/2.2.0/bazel-toolchains-2.2.0.tar.gz",
        "https://github.com/bazelbuild/bazel-toolchains/archive/2.2.0.tar.gz",
    ],
)

load("@bazel_toolchains//rules:rbe_repo.bzl", "rbe_autoconfig")

rbe_autoconfig(name = "rbe_default")

go_repository(
    name = "com_github_google_go_containerregistry",
    importpath = "github.com/google/go-containerregistry",
    sum = "h1:PTrxTL8TNRbZts4KqdJMsqRlrdjoiKFDq6MVitj8mPk=",
    version = "v0.0.0-20190829181151-21b2e01cec04",
)

# Start using distroless base
container_pull(
    name = "distroless_base_amd64",
    digest = "sha256:e7fa8d9d08846d634b16d4ac7d8ecac36b412bfeb1a13ce061183ff020551ba8",
    registry = "gcr.io",
    repository = "distroless/base",
)

container_pull(
    name = "distroless_base_arm64",
    digest = "sha256:c60be29941a0be6f748c8cf2e42832f95e9b73276042d3c44212af7cf4a152c9",
    registry = "gcr.io",
    repository = "distroless/base",
)

container_pull(
    name = "distroless_base_debug_amd64",
    digest = "sha256:c9e0f9309fcf71590eb58e4ee51aba280a2c7f513bd18ddf712924e3d98f7615",
    registry = "gcr.io",
    repository = "distroless/base",
)

container_pull(
    name = "distroless_base_debug_arm64",
    digest = "sha256:a50f1f26fc50ae5a14fee9efa88d7772898231b3bee950b13af5d07df3fe8364",
    registry = "gcr.io",
    repository = "distroless/base",
)
