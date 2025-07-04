project('xrdb', 'c', default_options: ['buildtype=debugoptimized', 'c_std=gnu99', 'warning_level=2'])

version = '1.2.3'
package_string = f'xrdb @version@'
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
funcs_to_check = [
  ['asprintf', 'HAVE_ASPRINTF'],
  ['mkstemp', 'HAVE_MKSTEMP'],
  ['reallocarray', 'HAVE_REALLOCARRAY'],
]
foreach fn : funcs_to_check
  if cc.has_function(fn[0])
    add_project_arguments('-D@0@'.format(fn[1]), language: 'c')
  endif
endforeach

add_project_arguments(
  '-D_DEFAULT_SOURCE', '-D_XOPEN_SOURCE=700L', f'-DPACKAGE_STRING="@package_string@"',
  language: 'c'
)
executable('xrdb', srcs, dependencies: deps)
