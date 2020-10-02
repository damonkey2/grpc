load("@bazel_skylib//rules:copy_file.bzl", "copy_file")

config_setting(
    name = "android",
    constraint_values = ["@platforms//os:android"],
)

config_setting(
    name = "freebsd",
    constraint_values = ["@platforms//os:freebsd"],
)

config_setting(
    name = "ios",
    constraint_values = ["@platforms//os:ios"],
)

config_setting(
    name = "macos",
    constraint_values = ["@platforms//os:macos"],
)

config_setting(
    name = "openbsd",
    constraint_values = ["@platforms//os:openbsd"],
)

config_setting(
    name = "tvos",
    constraint_values = ["@platforms//os:tvos"],
)

config_setting(
    name = "watchos",
    constraint_values = ["@platforms//os:watchos"],
)

config_setting(
    name = "windows",
    constraint_values = ["@platforms//os:windows"],
)

copy_file(
    name = "ares_build_h",
    src = "@com_github_grpc_grpc//third_party/cares:ares_build.h",
    out = "ares_build.h",
)

copy_file(
    name = "ares_config_h",
    src = select({
        ":android": "@com_github_grpc_grpc//third_party/cares:config_android/ares_config.h",
        ":ios": "@com_github_grpc_grpc//third_party/cares:config_darwin/ares_config.h",
        ":macos": "@com_github_grpc_grpc//third_party/cares:config_darwin/ares_config.h",
        ":tvos": "@com_github_grpc_grpc//third_party/cares:config_darwin/ares_config.h",
        ":watchos": "@com_github_grpc_grpc//third_party/cares:config_darwin/ares_config.h",
        ":freebsd": "@com_github_grpc_grpc//third_party/cares:config_freebsd/ares_config.h",
        ":openbsd": "@com_github_grpc_grpc//third_party/cares:config_openbsd/ares_config.h",
        ":windows": "@com_github_grpc_grpc//third_party/cares:config_windows/ares_config.h",
        "//conditions:default": "@com_github_grpc_grpc//third_party/cares:config_linux/ares_config.h",
    }),
    out = "ares_config.h",
)

cc_library(
    name = "ares",
    srcs = [
        "ares__close_sockets.c",
        "ares__get_hostent.c",
        "ares__read_line.c",
        "ares__timeval.c",
        "ares_android.c",
        "ares_cancel.c",
        "ares_create_query.c",
        "ares_data.c",
        "ares_destroy.c",
        "ares_expand_name.c",
        "ares_expand_string.c",
        "ares_fds.c",
        "ares_free_hostent.c",
        "ares_free_string.c",
        "ares_getenv.c",
        "ares_gethostbyaddr.c",
        "ares_gethostbyname.c",
        "ares_getnameinfo.c",
        "ares_getopt.c",
        "ares_getsock.c",
        "ares_init.c",
        "ares_library_init.c",
        "ares_llist.c",
        "ares_mkquery.c",
        "ares_nowarn.c",
        "ares_options.c",
        "ares_parse_a_reply.c",
        "ares_parse_aaaa_reply.c",
        "ares_parse_mx_reply.c",
        "ares_parse_naptr_reply.c",
        "ares_parse_ns_reply.c",
        "ares_parse_ptr_reply.c",
        "ares_parse_soa_reply.c",
        "ares_parse_srv_reply.c",
        "ares_parse_txt_reply.c",
        "ares_platform.c",
        "ares_process.c",
        "ares_query.c",
        "ares_search.c",
        "ares_send.c",
        "ares_strcasecmp.c",
        "ares_strdup.c",
        "ares_strsplit.c",
        "ares_strerror.c",
        "ares_timeout.c",
        "ares_version.c",
        "ares_writev.c",
        "bitncmp.c",
        "inet_net_pton.c",
        "inet_ntop.c",
        "windows_port.c",
    ],
    hdrs = [
        "ares.h",
        "ares_android.h",
        "ares_build.h",
        "ares_config.h",
        "ares_data.h",
        "ares_dns.h",
        "ares_getenv.h",
        "ares_getopt.h",
        "ares_inet_net_pton.h",
        "ares_iphlpapi.h",
        "ares_ipv6.h",
        "ares_library_init.h",
        "ares_llist.h",
        "ares_nowarn.h",
        "ares_platform.h",
        "ares_private.h",
        "ares_rules.h",
        "ares_setup.h",
        "ares_strcasecmp.h",
        "ares_strdup.h",
        "ares_strsplit.h",
        "ares_version.h",
        "ares_writev.h",
        "bitncmp.h",
        "config-win32.h",
        "nameser.h",
        "setup_once.h",
    ],
    copts = [
        "-D_GNU_SOURCE",
        "-D_HAS_EXCEPTIONS=0",
        "-DHAVE_CONFIG_H",
    ] + select({
        ":windows": [
            "-DNOMINMAX",
            "-D_CRT_SECURE_NO_DEPRECATE",
            "-D_CRT_NONSTDC_NO_DEPRECATE",
            "-D_WIN32_WINNT=0x0600",
        ],
        "//conditions:default": [],
    }),
    defines = ["CARES_STATICLIB"],
    includes = ["."],
    linkopts = select({
        ":windows": ["-defaultlib:ws2_32.lib"],
        "//conditions:default": [],
    }),
    linkstatic = 1,
    visibility = [
        "//visibility:public",
    ],
    alwayslink = 1,
)
