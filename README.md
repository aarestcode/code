# README #

All include paths are "from the root". You must change your code away from bracket <> search style to quotes "" search style. eg:
```
#include <Eigen/Core>
```
becomes
```
#include "third_party/eigen/Eigen/Core"
```

### How do I get set up? ###

```
git clone https://username@github.com/aarestcode/camera-code.git
```
* Dependencies:

This repo is built with Bazel. [Install docs here](https://bazel.build/versions/master/docs/install.html):

### Compiling ###
```
code$ bazel build test:test
```

### Cross-Compiling ###
```
code$ bazel build test:test --host_cpu=k9 --crosstool_top=//tools/arm_compiler:toolchain --cpu=sama5d3xek
```
