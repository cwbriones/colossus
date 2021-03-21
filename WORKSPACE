load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")

GRPC_SHA = "3e53dbe8213137d2c731ecd4d88ebd2948941d75"

# Imports basic Go rules for Bazel (e.g. go_binary)
http_archive(
    name = "io_bazel_rules_go",
    sha256 = "7c10271940c6bce577d51a075ae77728964db285dac0a46614a7934dc34303e6",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_go/releases/download/v0.26.0/rules_go-v0.26.0.tar.gz",
        "https://github.com/bazelbuild/rules_go/releases/download/v0.26.0/rules_go-v0.26.0.tar.gz",
    ],
)

# Imports the Gazelle tool for Go/Bazel
http_archive(
    name = "bazel_gazelle",
    sha256 = "62ca106be173579c0a167deb23358fdfe71ffa1e4cfdddf5582af26520f1c66f",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-gazelle/releases/download/v0.23.0/bazel-gazelle-v0.23.0.tar.gz",
        "https://github.com/bazelbuild/bazel-gazelle/releases/download/v0.23.0/bazel-gazelle-v0.23.0.tar.gz",
    ],
)

load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")
load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies", "go_repository")

go_rules_dependencies()

go_register_toolchains(version = "1.15.2")

gazelle_dependencies()

http_archive(
    name = "com_google_protobuf",
    sha256 = "985bb1ca491f0815daad825ef1857b684e0844dc68123626a08351686e8d30c9",
    strip_prefix = "protobuf-3.15.6",
    urls = ["https://github.com/protocolbuffers/protobuf/archive/v3.15.6.zip"],
)

load("@com_google_protobuf//:protobuf_deps.bzl", "protobuf_deps")

protobuf_deps()

# Imports Docker rules for Bazel (e.g. docker_image)
git_repository(
    name = "io_bazel_rules_docker",
    remote = "https://github.com/bazelbuild/rules_docker.git",
    tag = "v0.16.0"
)

# Import gRPC for C++
http_archive(
    name = "com_github_grpc_grpc",
    sha256 = "89bab58f7bd36f2826b0bde92ea5668324642fe281d636dd18025354586cb764",
    urls = [
        "https://github.com/grpc/grpc/archive/3e53dbe8213137d2c731ecd4d88ebd2948941d75.tar.gz",
    ],
    strip_prefix = "grpc-3e53dbe8213137d2c731ecd4d88ebd2948941d75",
)
load("@com_github_grpc_grpc//bazel:grpc_deps.bzl", "grpc_deps")
grpc_deps()
load("@com_github_grpc_grpc//bazel:grpc_extra_deps.bzl", "grpc_extra_deps")
grpc_extra_deps()

# Imports gRPC for Java rules (e.g. java_grpc_library)
git_repository(
    name = "io_grpc_grpc_java",
    commit = "e9065ab330aedd6b4d2dbc5623a66624dedbb596",
    remote = "https://github.com/grpc/grpc-java",
    shallow_since = "1615587718 -0800",
)

load("@io_grpc_grpc_java//:repositories.bzl", "grpc_java_repositories")
grpc_java_repositories()

# gRPC for Java dependencies (shorthand)
bind(
    name = "grpc-core",
    actual = "@io_grpc_grpc_java//core",
)

bind(
    name = "grpc-netty",
    actual = "@io_grpc_grpc_java//netty",
)

bind(
    name = "grpc-stub",
    actual = "@io_grpc_grpc_java//stub",
)

# Import Maven rules for Gradle conversion
RULES_JVM_EXTERNAL_TAG = "4.0"
RULES_JVM_EXTERNAL_SHA = "31701ad93dbfe544d597dbe62c9a1fdd76d81d8a9150c2bf1ecf928ecdf97169"

http_archive(
    name = "rules_jvm_external",
    strip_prefix = "rules_jvm_external-%s" % RULES_JVM_EXTERNAL_TAG,
    sha256 = RULES_JVM_EXTERNAL_SHA,
    url = "https://github.com/bazelbuild/rules_jvm_external/archive/%s.zip" % RULES_JVM_EXTERNAL_TAG,
)
load("@rules_jvm_external//:defs.bzl", "maven_install")

maven_install(
    artifacts = [
        "io.prometheus:simpleclient:0.10.0",
        "io.prometheus:simpleclient_common:0.10.0",
        "io.prometheus:simpleclient_httpserver:0.10.0",
        "me.dinowernli:java-grpc-prometheus:0.3.0",
    ],
    repositories = [
        "https://repo.maven.apache.org/maven2",
    ],
)

# # Loads Docker for Java rules (e.g. java_image)
# load(
#     "@io_bazel_rules_docker//java:image.bzl",
#     _java_image_repos = "repositories",
# )
#
# _java_image_repos()


# # Loads Docker rules for Bazel
load(
    "@io_bazel_rules_docker//go:image.bzl",
    _go_image_repos = "repositories",
)

_go_image_repos()

# Loads C++ Docker image rules
# load(
#     "@io_bazel_rules_docker//cc:image.bzl",
#     _cc_image_repos = "repositories",
# )

# _cc_image_repos()

# Gazelle-generated Go dependencies
go_repository(
    name = "com_github_inconshreveable_mousetrap",
    commit = "76626ae9c91c4f2a10f34cad8ce83ea42c93bb75",
    importpath = "github.com/inconshreveable/mousetrap",
)

go_repository(
    name = "com_github_spf13_cobra",
    commit = "a1f051bc3eba734da4772d60e2d677f47cf93ef4",
    importpath = "github.com/spf13/cobra",
)

go_repository(
    name = "com_github_spf13_pflag",
    commit = "583c0c0531f06d5278b7d917446061adc344b5cd",
    importpath = "github.com/spf13/pflag",
)

go_repository(
    name = "com_github_go_chi_chi",
    commit = "e83ac2304db3c50cf03d96a2fcd39009d458bc35",
    importpath = "github.com/go-chi/chi",
)

go_repository(
    name = "com_github_sirupsen_logrus",
    commit = "c155da19408a8799da419ed3eeb0cb5db0ad5dbc",
    importpath = "github.com/sirupsen/logrus",
)

go_repository(
    name = "org_golang_x_crypto",
    commit = "b49d69b5da943f7ef3c9cf91c8777c1f78a0cc3c",
    importpath = "golang.org/x/crypto",
)

go_repository(
    name = "org_golang_x_sys",
    commit = "cbbc999da32df943dac6cd71eb3ee39e1d7838b9",
    importpath = "golang.org/x/sys",
)

go_repository(
    name = "com_github_fsnotify_fsnotify",
    commit = "c2828203cd70a50dcccfb2761f8b1f8ceef9a8e9",
    importpath = "github.com/fsnotify/fsnotify",
)

go_repository(
    name = "com_github_hashicorp_hcl",
    commit = "ef8a98b0bbce4a65b5aa4c368430a80ddc533168",
    importpath = "github.com/hashicorp/hcl",
)

go_repository(
    name = "com_github_magiconair_properties",
    commit = "c3beff4c2358b44d0493c7dda585e7db7ff28ae6",
    importpath = "github.com/magiconair/properties",
)

go_repository(
    name = "com_github_mitchellh_mapstructure",
    commit = "00c29f56e2386353d58c599509e8dc3801b0d716",
    importpath = "github.com/mitchellh/mapstructure",
)

go_repository(
    name = "com_github_pelletier_go_toml",
    commit = "acdc4509485b587f5e675510c4f2c63e90ff68a8",
    importpath = "github.com/pelletier/go-toml",
)

go_repository(
    name = "com_github_spf13_afero",
    commit = "63644898a8da0bc22138abf860edaf5277b6102e",
    importpath = "github.com/spf13/afero",
)

go_repository(
    name = "com_github_spf13_cast",
    commit = "8965335b8c7107321228e3e3702cab9832751bac",
    importpath = "github.com/spf13/cast",
)

go_repository(
    name = "com_github_spf13_jwalterweatherman",
    commit = "7c0cea34c8ece3fbeb2b27ab9b59511d360fb394",
    importpath = "github.com/spf13/jwalterweatherman",
)

go_repository(
    name = "com_github_spf13_viper",
    commit = "b5e8006cbee93ec955a89ab31e0e3ce3204f3736",
    importpath = "github.com/spf13/viper",
)

go_repository(
    name = "in_gopkg_yaml_v2",
    commit = "5420a8b6744d3b0345ab293f6fcba19c978f1183",
    importpath = "gopkg.in/yaml.v2",
)

go_repository(
    name = "org_golang_x_text",
    commit = "f21a4dfb5e38f5895301dc265a8def02365cc3d0",
    importpath = "golang.org/x/text",
)

go_repository(
    name = "com_github_go_pg_pg",
    commit = "5b73ce88484575f3480edf393237f6bf79d5f166",
    importpath = "github.com/go-pg/pg",
)

go_repository(
    name = "com_github_jinzhu_inflection",
    commit = "04140366298a54a039076d798123ffa108fff46c",
    importpath = "github.com/jinzhu/inflection",
)

go_repository(
    name = "com_github_golang_protobuf",
    commit = "b4deda0973fb4c70b50d226b1af49f3da59f5265",
    importpath = "github.com/golang/protobuf",
)

go_repository(
    name = "org_golang_google_genproto",
    commit = "86e600f69ee4704c6efbf6a2a40a5c10700e76c2",
    importpath = "google.golang.org/genproto",
)

go_repository(
  name = "org_golang_google_grpc",
  importpath = "google.golang.org/grpc",
  tag = "v1.36.0"
)

go_repository(
    name = "org_golang_x_net",
    commit = "5f9ae10d9af5b1c89ae6904293b14b064d4ada23",
    importpath = "golang.org/x/net",
)

go_repository(
    name = "com_github_go_redis_redis",
    commit = "0f9028adf0837cf93c9705817493e5f6997cf026",
    importpath = "github.com/go-redis/redis",
)

go_repository(
    name = "com_github_unrolled_render",
    commit = "65450fb6b2d3595beca39f969c411db8f8d5c806",
    importpath = "github.com/unrolled/render",
)

go_repository(
    name = "com_github_beorn7_perks",
    commit = "3a771d992973f24aa725d07868b467d1ddfceafb",
    importpath = "github.com/beorn7/perks",
)

go_repository(
    name = "com_github_matttproud_golang_protobuf_extensions",
    commit = "c12348ce28de40eed0136aa2b644d0ee0650e56c",
    importpath = "github.com/matttproud/golang_protobuf_extensions",
)

go_repository(
    name = "com_github_prometheus_client_golang",
    commit = "c5b7fccd204277076155f10851dad72b76a49317",
    importpath = "github.com/prometheus/client_golang",
)

go_repository(
    name = "com_github_prometheus_client_model",
    commit = "99fa1f4be8e564e8a6b613da7fa6f46c9edafc6c",
    importpath = "github.com/prometheus/client_model",
)

go_repository(
    name = "com_github_prometheus_common",
    commit = "7600349dcfe1abd18d72d3a1770870d9800a7801",
    importpath = "github.com/prometheus/common",
)

go_repository(
    name = "com_github_prometheus_procfs",
    commit = "94663424ae5ae9856b40a9f170762b4197024661",
    importpath = "github.com/prometheus/procfs",
)

go_repository(
    name = "com_github_grpc_ecosystem_go_grpc_prometheus",
    commit = "c225b8c3b01faf2899099b768856a9e916e5087b",
    importpath = "github.com/grpc-ecosystem/go-grpc-prometheus",
)

go_repository(
    name = "com_github_caarlos0_env",
    commit = "1cddc31c48c56ecd700d873edb9fd5b6f5df922a",
    importpath = "github.com/caarlos0/env",
)
