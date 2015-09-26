# boot-less
[![Clojars Project](http://clojars.org/deraen/boot-less/latest-version.svg)](http://clojars.org/deraen/boot-less)

[Boot](https://github.com/boot-clj/boot) task to compile Less.

* Provides the `less` task
* For each `.main.less` in fileset creates equivalent `.css` file.
* Uses [Less4j](https://github.com/SomMeri/less4j) Java implementation of Less compiler through [less4clj clojure wrapper](https://github.com/Deraen/less4clj)
* For parallel leiningen plugin check [less-less4j](https://github.com/Deraen/lein-less4j/)

## Usage

```clj
[s source-map  bool "Create source-map for compiled CSS."
 c compression bool "Compress compiled CSS using simple compression."]
```

To create css file `public/css/main.css` have the less file on path `public/css/main.main.less` or use sift task to move the css file:
`(comp (less) (sift :move {#"main.css" "public/css/main.css"}))`

## Features

- Load imports from classpath
  - Loading order. `@import "{name}";` at `{path}`.
    1. check if file `{path}/{name}.less` exists
    2. try `(io/resource "{name}.less")`
    3. try `(io/resource "{path}/{name}.less")`
    4. check if webjars asset map contains `{name}`
      - Resource `META-INF/resources/webjars/{package}/{version}/{path}` can be referred using `{package}/{path}`
      - E.g. `bootstrap/less/bootstrap.less` => `META-INF/resources/webjars/bootstrap/3.3.1/less/bootstrap.less`
  - You should be able to depend on `[org.webjars/bootstrap "3.3.1"]`
    and use `@import "bootstrap/less/bootstrap";`
  - Use boot debug to find what is being loaded:
    `boot -vvv less`

## FAQ

### Log configuration

If you are using some logging stuff it might be that library used by
less4j will write lots of stuff to your log, then you should add the following
rule to your `logback.xml`:

```xml
  <logger name="org.apache.commons.beanutils.converters" level="INFO"/>
```

## License

Copyright © 2014-2015 Juho Teperi

Distributed under the Eclipse Public License either version 1.0 or (at your option) any later version.
