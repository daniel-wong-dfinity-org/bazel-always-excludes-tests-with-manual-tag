For example, the following command executes tests:

```
bazel test //... --test_tag_filters=manual
```

But this one does:

```
bazel test //:foo_test
```

You might think that one of the following commands would cause `//:bar_test` to
be executed, but all of these commands execute no tests:

```
bazel test //... --test_tag_filters=nightly,manual
bazel test //... --test_tag_filters=nightly
```

In order to make `bar_test` run, you must remove the `manual` tag. Once you do
that, then you only need `--test_tag_filters=nightly` to run `bar_test`; no need
to also pass `manual` to `--test_tag_filters`. In other words, once you remove
`manual` from `bar_test`, the following works:

```
bazel test //... --test_tag_filters=nightly
```