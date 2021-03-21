package(default_visibility = ["//visibility:public"])

load("@bazel_gazelle//:def.bzl", "gazelle")
load("@io_bazel_rules_docker//cc:image.bzl", "cc_image")
load("@io_bazel_rules_docker//go:image.bzl", "go_image")
load("@io_bazel_rules_docker//java:image.bzl", "java_image")
load("@io_bazel_rules_docker//container:container.bzl", "container_push")

DOCKER_REGISTRY_URL = "localhost:5000"

# A Gazelle executable for auto-generating Go BUILD definitions
# gazelle:prefix github.com/lucperkins/colossus
# This line is necessary to keep Gazelle from using the vendored gRPC for Go library
# gazelle:exclude vendor
gazelle(name = "gazelle")

# A Docker image for the web service (Linux binary)
go_image(
    name = "colossus-web",
    binary = "//web:web_linux_bin",
)

# A Docker image for the auth service (Linux binary)
go_image(
    name = "colossus-auth",
    binary = "//auth:auth_linux_bin",
)

# A Docker image for the data service
java_image(
    name = "colossus-data",
    main_class = "colossus.DataHandler",
    runtime_deps = ["//data:data_java_lib"],
)

# A Docker image for the userinfo C++ service
cc_image(
    name = "colossus-userinfo",
    binary = "//userinfo:userinfo-bin",
)

container_push(
    name = "auth-push",
    image = ":colossus-auth",
    format = "Docker",
    registry = DOCKER_REGISTRY_URL,
    repository = "colossus/auth",
    tag = "{BUILD_TIMESTAMP}",
)

container_push(
    name = "web-push",
    image = ":colossus-web",
    format = "Docker",
    registry = DOCKER_REGISTRY_URL,
    repository = "colossus/web",
    tag = "{BUILD_TIMESTAMP}",
)

container_push(
    name = "data-push",
    image = ":colossus-data",
    format = "Docker",
    registry = DOCKER_REGISTRY_URL,
    repository = "colossus/data",
    tag = "{BUILD_TIMESTAMP}",
)

container_push(
    name = "userinfo-push",
    image = ":colossus-userinfo",
    format = "Docker",
    registry = DOCKER_REGISTRY_URL,
    repository = "colossus/userinfo",
    tag = "{BUILD_TIMESTAMP}",
)
