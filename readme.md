# NATS.c

This is the [NATS C client library][nats.c], packaged for [Zig](https://ziglang.org/).

## Status

This library only explicitly supports Linux, macOS, and Windows operating systems. Building for other platforms is currently untested, so your mileage may vary.

## Zig Bindings

The following projects provide Zig language bindings to the NATS.c library:

- [`epicyclic-dev/nats-client`][epicyclic-dev-bindings]

## Usage

First, update your `build.zig.zon`:

```sh
# Initialize a `zig build` project if you haven't already
zig init
# replace <refname> with the version you want to use, e.g. 3.8.2
zig fetch --save git+https://github.com/allyourcodebase/nats.c.git#<refname>
```

You can then import `nats_c` in your `build.zig` with:

```zig
const nats_c_dep = b.dependency("nats_c", .{
    .target = target,
    .optimize = optimize,
    .@"enable-tls" = true, // enable SSL/TLS support
    .@"force-host-verify" = true, // force hostname verification for TLS connections
    .@"enable-streaming" = true, // build with support for NATS streaming extensions
});
your_exe.linkLibrary(nats_c_dep.artifact("nats_c"));
```

## Dependencies

The NATS.c library has two optional dependencies:

- [`libressl`][libressl] when building with `enable-tls`
- [`protobuf-c`][protobuf-c] when building with `enable-streaming`

These dependencies are currently automatically retrieved and compiled as static libraries by the Zig build system.

## Version Support Matrix

|  Refname | NATS.c Version | Zig `0.12.x` | Zig `0.13.x` | Zig `0.14.0-dev` |
|----------|----------------|--------------|--------------|------------------|
| `3.8.2`  | `3.8.2`        | ✅           | ✅          | ✅              |

[nats.c]: https://github.com/nats-io/nats.c
[libressl]: https://github.com/allyourcodebase/libressl
[protobuf-c]: https://github.com/allyourcodebase/protobuf-c
[epicyclic-dev-bindings]: https://github.com/epicyclic-dev/nats-client
