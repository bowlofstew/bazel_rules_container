load("@bazel_rules_container//container:test.bzl", "container_test")

container_test(
    name = "nodejs",
    size = "small",
    files = [
        "project/index.js",
        "project/package.json",
    ],
    golden = "output.txt",
    image = "//nodejs",
    test = "test.sh",
)
