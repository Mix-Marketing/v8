# Note: The buildbots evaluate this file with CWD set to the parent
# directory and assume that the root of the checkout is in ./v8/, so
# all paths in here must match this assumption.

vars = {
  "chromium_url": "https://chromium.googlesource.com",
}

deps = {
  "v8/build":
    Var("chromium_url") + "/chromium/src/build.git" + "@" + "b3765543a0e439f71548f86a783a399e0c121a4f",
  "v8/tools/gyp":
    Var("chromium_url") + "/external/gyp.git" + "@" + "d61a9397e668fa9843c4aa7da9e79460fe590bfb",
  "v8/third_party/icu":
    Var("chromium_url") + "/chromium/deps/icu.git" + "@" + "08cb956852a5ccdba7f9c941728bb833529ba3c6",
  "v8/third_party/instrumented_libraries":
    Var("chromium_url") + "/chromium/src/third_party/instrumented_libraries.git" + "@" + "644afd349826cb68204226a16c38bde13abe9c3c",
  "v8/buildtools":
    Var("chromium_url") + "/chromium/buildtools.git" + "@" + "f6d165d9d842ddd29056c127a5f3a3c5d8e0d2e3",
  "v8/base/trace_event/common":
    Var("chromium_url") + "/chromium/src/base/trace_event/common.git" + "@" + "65d1d42a5df6c0a563a6fdfa58a135679185e5d9",
  "v8/third_party/jinja2":
    Var("chromium_url") + "/chromium/src/third_party/jinja2.git" + "@" + "d34383206fa42d52faa10bb9931d6d538f3a57e0",
  "v8/third_party/markupsafe":
    Var("chromium_url") + "/chromium/src/third_party/markupsafe.git" + "@" + "8f45f5cfa0009d2a70589bcda0349b8cb2b72783",
  "v8/tools/swarming_client":
    Var('chromium_url') + '/infra/luci/client-py.git' + '@' + "5e8001d9a710121ce7a68efd0804430a34b4f9e4",
  "v8/testing/gtest":
    Var("chromium_url") + "/external/github.com/google/googletest.git" + "@" + "6f8a66431cb592dad629028a50b3dd418a408c87",
  "v8/testing/gmock":
    Var("chromium_url") + "/external/googlemock.git" + "@" + "0421b6f358139f02e102c9c332ce19a33faf75be",
  "v8/test/benchmarks/data":
    Var("chromium_url") + "/v8/deps/third_party/benchmarks.git" + "@" + "05d7188267b4560491ff9155c5ee13e207ecd65f",
  "v8/test/mozilla/data":
    Var("chromium_url") + "/v8/deps/third_party/mozilla-tests.git" + "@" + "f6c578a10ea707b1a8ab0b88943fe5115ce2b9be",
  "v8/test/test262/data":
    Var("chromium_url") + "/external/github.com/tc39/test262.git" + "@" + "290799bbeeba86245a355894b6ff2bb33d946d9e",
  "v8/test/test262/harness":
    Var("chromium_url") + "/external/github.com/test262-utils/test262-harness-py.git" + "@" + "0f2acdd882c84cff43b9d60df7574a1901e2cdcd",
  "v8/tools/clang":
    Var("chromium_url") + "/chromium/src/tools/clang.git" + "@" + "66be66dcb7169e736d56d6fc2b53a7d6dac87ac4",
  "v8/test/wasm-js":
    Var("chromium_url") + "/external/github.com/WebAssembly/spec.git" + "@" + "4f1d3114157e6459d8a06e7d8fcc8fc90288cd85",
}

deps_os = {
  "android": {
    "v8/third_party/android_tools":
      Var("chromium_url") + "/android_tools.git" + "@" + "ca9dc7245b888c75307f0619e4a39fb46a82de66",
    "v8/third_party/catapult":
      Var('chromium_url') + "/catapult.git" + "@" + "8ec7b14edf48a27389a11c5af3bc14991eb28152",
  },
}

recursedeps = [
  "v8/buildtools",
  "v8/third_party/android_tools",
]

include_rules = [
  # Everybody can use some things.
  "+include",
  "+unicode",
  "+third_party/fdlibm",
]

# checkdeps.py shouldn't check for includes in these directories:
skip_child_includes = [
  "build",
  "gypfiles",
  "third_party",
]

hooks = [
  {
    # This clobbers when necessary (based on get_landmines.py). It must be the
    # first hook so that other things that get/generate into the output
    # directory will not subsequently be clobbered.
    'name': 'landmines',
    'pattern': '.',
    'action': [
        'python',
        'v8/gypfiles/landmines.py',
    ],
  },
  # Pull clang-format binaries using checked-in hashes.
  {
    "name": "clang_format_win",
    "pattern": ".",
    "action": [ "download_from_google_storage",
                "--no_resume",
                "--platform=win32",
                "--no_auth",
                "--bucket", "chromium-clang-format",
                "-s", "v8/buildtools/win/clang-format.exe.sha1",
    ],
  },
  {
    "name": "clang_format_mac",
    "pattern": ".",
    "action": [ "download_from_google_storage",
                "--no_resume",
                "--platform=darwin",
                "--no_auth",
                "--bucket", "chromium-clang-format",
                "-s", "v8/buildtools/mac/clang-format.sha1",
    ],
  },
  {
    "name": "clang_format_linux",
    "pattern": ".",
    "action": [ "download_from_google_storage",
                "--no_resume",
                "--platform=linux*",
                "--no_auth",
                "--bucket", "chromium-clang-format",
                "-s", "v8/buildtools/linux64/clang-format.sha1",
    ],
  },
  {
    'name': 'gcmole',
    'pattern': '.',
    'action': [
        'python',
        'v8/tools/gcmole/download_gcmole_tools.py',
    ],
  },
  {
    'name': 'jsfunfuzz',
    'pattern': '.',
    'action': [
        'python',
        'v8/tools/jsfunfuzz/download_jsfunfuzz.py',
    ],
  },
  # Pull luci-go binaries (isolate, swarming) using checked-in hashes.
  {
    'name': 'luci-go_win',
    'pattern': '.',
    'action': [ 'download_from_google_storage',
                '--no_resume',
                '--platform=win32',
                '--no_auth',
                '--bucket', 'chromium-luci',
                '-d', 'v8/tools/luci-go/win64',
    ],
  },
  {
    'name': 'luci-go_mac',
    'pattern': '.',
    'action': [ 'download_from_google_storage',
                '--no_resume',
                '--platform=darwin',
                '--no_auth',
                '--bucket', 'chromium-luci',
                '-d', 'v8/tools/luci-go/mac64',
    ],
  },
  {
    'name': 'luci-go_linux',
    'pattern': '.',
    'action': [ 'download_from_google_storage',
                '--no_resume',
                '--platform=linux*',
                '--no_auth',
                '--bucket', 'chromium-luci',
                '-d', 'v8/tools/luci-go/linux64',
    ],
  },
  # Pull GN using checked-in hashes.
  {
    "name": "gn_win",
    "pattern": ".",
    "action": [ "download_from_google_storage",
                "--no_resume",
                "--platform=win32",
                "--no_auth",
                "--bucket", "chromium-gn",
                "-s", "v8/buildtools/win/gn.exe.sha1",
    ],
  },
  {
    "name": "gn_mac",
    "pattern": ".",
    "action": [ "download_from_google_storage",
                "--no_resume",
                "--platform=darwin",
                "--no_auth",
                "--bucket", "chromium-gn",
                "-s", "v8/buildtools/mac/gn.sha1",
    ],
  },
  {
    "name": "gn_linux",
    "pattern": ".",
    "action": [ "download_from_google_storage",
                "--no_resume",
                "--platform=linux*",
                "--no_auth",
                "--bucket", "chromium-gn",
                "-s", "v8/buildtools/linux64/gn.sha1",
    ],
  },
  {
    "name": "wasm_spec_tests",
    "pattern": ".",
    "action": [ "download_from_google_storage",
                "--no_resume",
                "--no_auth",
                "-u",
                "--bucket", "v8-wasm-spec-tests",
                "-s", "v8/test/wasm-spec-tests/tests.tar.gz.sha1",
    ],
  },
  {
    "name": "closure_compiler",
    "pattern": ".",
    "action": [ "download_from_google_storage",
                "--no_resume",
                "--no_auth",
                "-u",
                "--bucket", "chromium-v8-closure-compiler",
                "-s", "v8/src/inspector/build/closure-compiler.tar.gz.sha1",
    ],
  },
  {
    # Downloads the current stable linux sysroot to build/linux/ if needed.
    # This sysroot updates at about the same rate that the chrome build deps
    # change.
    'name': 'sysroot',
    'pattern': '.',
    'action': [
        'python',
        'v8/build/linux/sysroot_scripts/install-sysroot.py',
        '--running-as-hook',
    ],
  },
  {
    # Pull sanitizer-instrumented third-party libraries if requested via
    # GYP_DEFINES.
    'name': 'instrumented_libraries',
    'pattern': '\\.sha1',
    'action': [
        'python',
        'v8/third_party/instrumented_libraries/scripts/download_binaries.py',
    ],
  },
  {
    # Update the Windows toolchain if necessary.
    'name': 'win_toolchain',
    'pattern': '.',
    'action': ['python', 'v8/build/vs_toolchain.py', 'update'],
  },
  # Pull binutils for linux, enabled debug fission for faster linking /
  # debugging when used with clang on Ubuntu Precise.
  # https://code.google.com/p/chromium/issues/detail?id=352046
  {
    'name': 'binutils',
    'pattern': 'v8/third_party/binutils',
    'action': [
        'python',
        'v8/third_party/binutils/download.py',
    ],
  },
  {
    # Pull clang if needed or requested via GYP_DEFINES.
    # Note: On Win, this should run after win_toolchain, as it may use it.
    'name': 'clang',
    'pattern': '.',
    'action': ['python', 'v8/tools/clang/scripts/update.py', '--if-needed'],
  },
  {
    # A change to a .gyp, .gypi, or to GYP itself should run the generator.
    "pattern": ".",
    "action": ["python", "v8/gypfiles/gyp_v8", "--running-as-hook"],
  },
]
