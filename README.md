loading namespaces from user.clj seems have gotten slower on recent
jdks. it is most noticible with macro heavy code (see core.async).

foo.clj loads clojure.core.async then exits. the deps.edn has no
paths, :user alias adds a user.clj on the classpath which loads
foo.clj

## Bad

openjdk version "12" 2019-03-19
OpenJDK Runtime Environment 19.3 (build 12+30)
OpenJDK 64-Bit Server VM 19.3 (build 12+30, mixed mode, sharing)

```
$  clj -A:user                           
"Elapsed time: 18004.782405 msecs"
```

```
$ clj foo.clj                           
"Elapsed time: 7749.896518 msecs"
```

## Bad

openjdk version "11.0.2" 2019-01-15 LTS
OpenJDK Runtime Environment Zulu11.29+3-CA (build 11.0.2+7-LTS)
OpenJDK 64-Bit Server VM Zulu11.29+3-CA (build 11.0.2+7-LTS, mixed mode)

```
$ clj -A:user                           
"Elapsed time: 17301.514015 msecs"
```

```
$ clj foo.clj                           
"Elapsed time: 7875.408021 msecs"
```

## Good

openjdk version "1.8.0_192"
OpenJDK Runtime Environment (build 1.8.0_192-b12)
OpenJDK 64-Bit Server VM (build 25.192-b12, mixed mode)

```
$ clj -A:user                           
"Elapsed time: 6614.288118 msecs"
```

```
$ clj foo.clj                           
"Elapsed time: 7434.902931 msecs"
```

## Good

openjdk version "1.8.0_72"
OpenJDK Runtime Environment (Zulu 8.13.0.5-linux64) (build 1.8.0_72-b15)
OpenJDK 64-Bit Server VM (Zulu 8.13.0.5-linux64) (build 25.72-b15, mixed mode)

```
$ clj -A:user                           
"Elapsed time: 5885.804005 msecs"
```

```
$ clj foo.clj                           
"Elapsed time: 7512.793377 msecs"
```
