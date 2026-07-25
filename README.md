### Description
These [`Bazel`](https://bazel.build/) files help migrate the [xxhash](https://xxhash.com/) repository, which is
described as an extremely fast non-cryptographic hash algorithm, working at RAM speed limit. It is proposed in four
flavors (XXH32, XXH64, XXH3_64bits and XXH3_128bits). The latest variant, XXH3, offers improved performance across the
board, especially on small data.

The official GitHub repository for `xxhash` resides here: https://github.com/cyan4973/xxhash.

This repository provides the content for migrating the [`libxxhash`](
    https://github.com/Cyan4973/xxHash/blob/82cead715cbfddd9e6093db8df95155077ce6e64/build/cmake/CMakeLists.txt#L87-#L102
    ) library, and the [`xxhsum`](
        https://github.com/Cyan4973/xxHash/blob/82cead715cbfddd9e6093db8df95155077ce6e64/build/cmake/CMakeLists.txt#L115-#L134
        ) executable to [`Bazel`](https://bazel.build/). In addition to the library and executable, we also provide the
        files required to migrate the [`test_filename_escape`](
            https://github.com/Cyan4973/xxHash/blob/82cead715cbfddd9e6093db8df95155077ce6e64/tests/Makefile#L104) and
            [`test_sanity`](
                https://github.com/Cyan4973/xxHash/blob/82cead715cbfddd9e6093db8df95155077ce6e64/tests/Makefile#L115)
                unit tests.

### Notes
1. Please note that these files were designed for a specific instance of `xxHash`, i.e., `82cead7`.
2. There is room for improvement within this repository, e.g., splitting the GCC toolchain into its own package etc.
   However, this is **out of scope** for the purposes of this example.
