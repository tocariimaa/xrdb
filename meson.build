project('xrdb', 'c',
  default_options: ['buildtype=debugoptimized', 'c_std=gnu99', 'warning_level=2'],
  version: '1.2.3',
)

package_string = 'xrdb @0@'.format(meson.project_version())
cc = meson.get_compiler('c')

srcs = ['xrdb.c']
deps = [
  cc.find_library('X11', required: true),
  cc.find_library('Xmu', required: true),
]

cpp_path = get_option('cpp')
if cpp_path != ''
  add_project_arguments(f'-DCPP="@cpp_path@"', language: 'c')
endif

# Check for the presence of these C stdlib functions
funcs_to_check = ['asprintf', 'reallocarray']
foreach fn : funcs_to_check
  if cc.has_function(fn)
    add_project_arguments('-DHAVE_@0@'.format(fn.to_upper()), language: 'c')
  endif
endforeach

add_project_arguments(
  '-D_DEFAULT_SOURCE', '-D_XOPEN_SOURCE=700L', f'-DPACKAGE_STRING="@package_string@"',
  language: 'c'
)
executable('xrdb', srcs, dependencies: deps)
