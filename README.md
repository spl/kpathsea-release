# Kpathsea Releases

[Kpathsea] is a library to do path searching. It is part of the TeXLive
distribution.

[Kpathsea]: https://tug.org/kpathsea/

This repository is a collection of standalone Kpathsea release archives.
Installing Kpathsea without the rest of the TeXLive distribution is not
straightforward, and it is needed for [dvisvgm]. While dvisvgm is also included
with TeXLive, that version is generally very old. So, I started this repository
to collect Kpathsea releases to ease installation of newer versions of dvisvgm,
especially on macOS where the Kpathsea library is not available.

[dvisvgm]: https://github.com/mgieseki/dvisvgm

## Working with release archives

### Creating

To create a new release archive, follow these steps:

1. Find the revision of the release by looking through the [changes to
   `c-auto.in`] in the TeXLive svn repository.

   For example, [this diff] shows that version 6.3.0 (see `KPSEVERSION`)
   was released at revision 46759.

2. Run the script in this repository with the version and revision as
   arguments.

   For example:

   ```
   $ ./create 6.3.0 46759
   ```

3. Commit the created file to the repository.

   For example:

   ```
   $ git add kpathsea-6.3.0.tar.gz
   $ git commit -m 'Add kpathsea-6.3.0.tar.gz'
   ```

[changes to `c-auto.in`]: https://www.tug.org/svn/texlive/trunk/Build/source/texk/kpathsea/c-auto.in?sortby=date&view=log
[this diff]: https://www.tug.org/svn/texlive/trunk/Build/source/texk/kpathsea/c-auto.in?r1=46545&r2=46759

### Testing

After creating a release archive, test it for building using the `test` script
in this repository.

For example, assuming you created the release archive `kpathsea-6.3.0.tar.gz`,
test it with:

```
$ ./test kpathsea-6.3.0.tar.gz
```

### Building

To build a release archive, follow these steps:

1. Extract the archive.

   For example:

   ```
   $ tar xzf kpathsea-6.3.0.tar.gz
   ```

2. Navigate to the `kpathsea` directory.

   For example:

   ```
   $ cd kpathsea-6.3.0/texk/kpathsea
   ```

3. Configure, build, and (optionally) install.

   For example:

   ```
   $ ./configure && make && make install
   ```

For `./configure` options, run `./configure --help`. In particular, you probably
want to use `--prefix=<path>` to configure the installation directory to
something other than the default `/usr/local`.

## Background

The process for extracting Kpathsea from the TexLive distribution and building
it was initially informed by [this Gist] and [this blog entry] by [Toby
Fleming]. I use `svn` instead of `rsync` to check out specific revisions.

[this Gist]: https://gist.github.com/tobywf/aeeeee63053aaaa841b4032963406684
[this blog entry]: https://tobywf.com/2017/04/build-dvisvgm-kpathsea-on-macos/
[Toby Fleming]: https://tobywf.com/
