This repository forms a test scenario for the following eslint issue:

https://github.com/eslint/eslint/issues/4606

Only src/foo/bar/baz.js is a real file
Three different symlinks exist in src linking to the each level of directory and the file.

Expected output (not following any symlinks)

```
eslint-test$ eslint src --rule "{no-unused-vars:2}"

/Users/ameighc/src/eslint-test/src/foo/bar/baz.js
  1:5  error  'badjs' is assigned a value but never used  no-unused-vars

✖ 1 problem (1 errors, 0 warnings)
```

Expected output (following all symlinks)

```
eslint-test$ eslint src --rule "{no-unused-vars:2}"

/Users/ameighc/src/eslint-test/src/barlink/baz.js
  1:5  error  'badjs' is assigned a value but never used  no-unused-vars

/Users/ameighc/src/eslint-test/src/bazlink.js
  1:5  error  'badjs' is assigned a value but never used  no-unused-vars

/Users/ameighc/src/eslint-test/src/foo/bar/baz.js
  1:5  error  'badjs' is assigned a value but never used  no-unused-vars

/Users/ameighc/src/eslint-test/src/foolink/bar/baz.js
  1:5  error  'badjs' is assigned a value but never used  no-unused-vars

✖ 4 problems (4 errors, 0 warnings)
```

Actual output (eslint v3.19.0)

```
eslint-test$ eslint src --rule "{no-unused-vars:2}"

/Users/ameighc/src/eslint-test/src/barlink/baz.js
  1:5  error  'badjs' is assigned a value but never used  no-unused-vars

/Users/ameighc/src/eslint-test/src/bazlink.js
  1:5  error  'badjs' is assigned a value but never used  no-unused-vars

/Users/ameighc/src/eslint-test/src/foo/bar/baz.js
  1:5  error  'badjs' is assigned a value but never used  no-unused-vars

✖ 3 problems (3 errors, 0 warnings)
```

