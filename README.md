# boot-less
[![Clojars Project](http://clojars.org/deraen/boot-less/latest-version.svg)](http://clojars.org/deraen/boot-less)

# [Moved to Deraen/less4clj](https://github.com/Deraen/less4clj)

[Boot](https://github.com/boot-clj/boot) task to compile Less.

* Provides the `less` task
* For each `.main.less` in fileset creates equivalent `.css` file.
* Uses [Less4j](https://github.com/SomMeri/less4j) Java implementation of Less compiler through [less4clj clojure wrapper](https://github.com/Deraen/less4clj)
* For parallel leiningen plugin check [less-less4j](https://github.com/Deraen/lein-less4j/)
* For parallel [sass](http://sass-lang.com/) task check [boot-sass](https://github.com/Deraen/boot-sass)

## Usage

```clj
[s source-map  bool "Create source-map for compiled CSS."
 c compression bool "Compress compiled CSS using simple compression."]
```

To create css file `public/css/main.css` have the less file on path `public/css/main.main.less` or use sift task to move the css file:
`(comp (less) (sift :move {#"main.css" "public/css/main.css"}))`

## License

Copyright © 2014-2015 Juho Teperi

Distributed under the Eclipse Public License either version 1.0 or (at your option) any later version.
