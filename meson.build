# Copyright (c) 2024-2025 fei_cong (https://github.com/feicong/ebpf-course)
project('libbpf', 'c', version: 'v1.5.0')

libbpf_extra_cflags = [
  '-D__user=',
  '-D__force=',
  '-D__poll_t=unsigned',
]

output_dir = 'output'

libbpf_sources = files(
  'src/bpf.c',
  'src/bpf_prog_linfo.c',
  'src/btf.c',
  'src/btf_dump.c',
  'src/btf_iter.c',
  'src/btf_relocate.c',
  'src/elf.c',
  'src/features.c',
  'src/gen_loader.c',
  'src/hashmap.c',
  'src/libbpf.c',
  'src/libbpf_errno.c',
  'src/libbpf_probes.c',
  'src/linker.c',
  'src/netlink.c',
  'src/nlattr.c',
  'src/relo_core.c',
  'src/ringbuf.c',
  'src/str_error.c',
  'src/strset.c',
  'src/usdt.c',
  'src/zip.c'
)

libbpf_static = static_library(
  'bpf_static',
  sources: libbpf_sources,
  c_args: libbpf_extra_cflags,
  include_directories: include_directories('include', 'include/uapi', 'src'),
  install: true,
)

libbpf_dep = declare_dependency(
  link_with: [libbpf_static],
  include_directories: include_directories('.'),
)

dep_libelf = dependency('libelf', fallback: ['libelf', 'libelf_dep'])
dep_zlib = dependency('zlib', fallback: ['zlib', 'zlib_dep'])

libbpf = library(
  'bpf',
  sources: libbpf_sources,
  c_args: libbpf_extra_cflags,
  include_directories: include_directories('include', 'include/uapi', 'src'),
  dependencies: [dep_libelf, dep_zlib],
  install: true,
)

pkg = import('pkgconfig')
pkg.generate(
  name: meson.project_name(),
  description: 'eBPF library',
  version: meson.project_version(),
  url: 'https://github.com/libbpf/libbpf',
  libraries: libbpf,
  libraries_private: libbpf_static,
  subdirs: ['libbpf'],
)

meson.override_dependency('libbpf', libbpf_dep)


