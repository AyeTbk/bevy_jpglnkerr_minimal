This is a minimal reproduction of bevyengine/bevy#14117

# Project structure
The top level crate is a basic executable which depends on a dynamically linked crate (`repro_dylib`, which mimics `bevy_dylib`).
The `repro_dylib` crate depends on the `repro_internal` crate (which mimics `bevy_internal`) which itself depends on the `repro_jpeg` crate (which mimics `zune-jpeg`).

`repro_jpeg` is exported by `repro_internal`, and then re-exported by `repro_dylib`.

When `repro_jpeg` has a crate-type of `"cdylib"`, linking of the basic executable fails. Otherwise, it succeeds.
