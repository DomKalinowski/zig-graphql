# 0.4.0

The `send` function is now designed to return the raw body. A new function, `splitAndParse`, has been added to perform the previous `send` operation. Due to incompatible API changes, the version has been bumped from 0.3.0 to 0.4.0.

# 0.3.0

Upgrade to zig 0.14.1, current stable. Changes in the project definition (`build.zig.zon`) are incompatible with the previous version, resulting in a version bump from 0.2.2 to 0.3.0.

# 0.2.2

Upgrade to zig 0.13.0, current stable. No breaking changes.

# 0.2.1

Fix build.zig.zon package name, previously "gql" and now "graphql".

# 0.2.0

Upgrade to zig 0.12.0, current stable

The main changes were artifacts of the [0.12.0](https://ziglang.org/download/0.12.0/release-notes.html) and build configuration changes. Because these were both breaking changes the new min supported zig version is 0.12.0. See the readme for the latest install notes.

# 0.1.0

Initial version

## 📼 installing

```zig
.{
    .name = "my-app",
    .version = "0.1.0",
    .dependencies = .{
        // 👇 declare dep properties
        .graphql = .{
            // 👇 uri to download
            .url = "https://github.com/softprops/zig-graphql/archive/refs/tags/v0.1.0.tar.gz",
            // 👇 hash verification
            .hash = "...",
        },
    },
}
```

```zig
const std = @import("std");

pub fn build(b: *std.Build) void {
    const target = b.standardTargetOptions(.{});

    const optimize = b.standardOptimizeOption(.{});
    // 👇 de-reference graphql dep from build.zig.zon
     const graphql = b.dependency("graphql", .{
        .target = target,
        .optimize = optimize,
    });
    var exe = b.addExecutable(.{
        .name = "your-exe",
        .root_source_file = .{ .path = "src/main.zig" },
        .target = target,
        .optimize = optimize,
    });
    // 👇 add the graphql module to executable
    exe.addModule("graphql", graphql.module("graphql"));

    b.installArtifact(exe);
}
```
