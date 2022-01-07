project('libbencode', 'c',
	default_options : [
		'warning_level=3',
		'werror=false',
		'debug=false',
		'optimization=2',
		'c_std=c2x', 'build.c_std=c2x'
		],
	license: 'Apache License',
	version: '1.0.0',
)
project_description = 'A p2p messaging library.'
add_project_arguments('-Wpedantic', language : 'c')
add_project_arguments('-Wshadow', language : 'c')


project_headers = [
	'bencode.h'
]

project_source_files = [
	'bencode.c'
]

install_headers(project_headers)

project_target=library('bencode', project_source_files)


project_dep = declare_dependency(
	include_directories: ['.'],
	link_with : project_target,
)

set_variable(meson.project_name() + '_dep', project_dep)
if meson.version().version_compare('>=0.54.0')
	meson.override_dependency(meson.project_name(), project_dep)
endif

# Make this library usable from the system's package manager.
install_headers(project_headers, subdir:meson.project_name())

pkg_mod = import('pkgconfig')
pkg_mod.generate(
	name : meson.project_name(),
	filebase : meson.project_name(),
	description : project_description,
	subdirs : meson.project_name(),
)
