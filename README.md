# bug-report-clj-kondo-misplaced-reports

I'm using clj-kondo v2021.08.06.

All linting issues in this repo are in the file `dir-1/user.clj`, but linting gives some warnings that mention the wrong file:
```
$ clj-kondo --lint dir-1 dir-2
dir-1/user.clj:4:5: warning: namespace clojure.string is required but never used
dir-2/another_ns.clj:3:24: warning: use alias or :refer
dir-2/another_ns.clj:4:28: warning: #'clojure.string/blank? is referred but never used
linting took 53ms, errors: 0, warnings: 3
```

If I lint only `dir-1`, the reports are good:

```
$ clj-kondo --lint dir-1
dir-1/user.clj:3:24: warning: use alias or :refer
dir-1/user.clj:4:5: warning: namespace clojure.string is required but never used
dir-1/user.clj:4:28: warning: #'clojure.string/blank? is referred but never used
linting took 45ms, errors: 0, warnings: 3
```

If I rename the `user.clj` file (to any new name I have tried), the reports are good. For example:

```
$ clj-kondo --lint dir-1 dir-2
dir-1/xxxx.clj:3:24: warning: use alias or :refer
dir-1/xxxx.clj:4:5: warning: namespace clojure.string is required but never used
dir-1/xxxx.clj:4:28: warning: #'clojure.string/blank? is referred but never used
linting took 52ms, errors: 0, warnings: 3
```
