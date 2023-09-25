# CMake 
[back to main index](../README.md)

## General
- running CMake without any arguments runs configure phase
    - `cmake [<options>] -B <path-to-build> [-S <path-to-source>]`
    - `cmake [<options>] <path-to-source | path-to-existing-build>`
- running CMake configure with preset (from build dir): `cmake --preset=<preset_name> .`
- running CMake build phase: `cmake --build <build_dir> [--config <Config>]`
