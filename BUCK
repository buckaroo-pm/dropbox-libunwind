load('//:subdir_glob.bzl', 'subdir_glob')

genrule(
  name = 'libunwind-common-h',
  out = 'libunwind-common.h',
  srcs = [
    'include/libunwind-common.h.in',
  ],
  cmd = \
    'cat $SRCS | sed -e \'s/@PKG_MAJOR@/1/g\' | ' +
    'sed -e \'s/@PKG_MINOR@/1/g\' | ' +
    'sed -e \'s/@PKG_EXTRA@//g\' > $OUT',
)

linux_srcs = glob([
  'src/os-linux.c',
  'src/x86_64/*-linux.c',
  'src/coredump/**/*.c',
  'src/setjpm/**/*.c',
  'src/unwind/**/*.c',
], exclude = [
  'src/coredump/_UCD_access_reg_freebsd.c',
])

linux_exported_headers = {
  'libunwind.h': 'include/libunwind-x86_64.h',
  'dwarf-config.h': 'include/tdep-x86_64/dwarf-config.h',
  'libunwind-common.h': ':libunwind-common-h',
  'tdep/libunwind_i.h': 'include/tdep-x86_64/libunwind_i.h',
}

cxx_library(
  name = 'unwind',
  header_namespace = '',
  exported_headers = subdir_glob([
    ('include', '**/*.h'),
  ]),
  exported_platform_headers = [
    ('linux.*', linux_exported_headers),
  ],
  headers = subdir_glob([
    ('src', '**/*.h'),
  ]),
  platform_srcs = [
    ('linux.*', linux_srcs),
  ],
  visibility = [
    'PUBLIC',
  ],
)
