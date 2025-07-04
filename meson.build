project('xrdb', 'c', default_options: ['buildtype=debugoptimized', 'c_std=gnu99', 'warning_level=2'])

version = '1.2.3'
package_string = f'xrdb @version@'
cc = meson.get_compiler('c')

srcs = ['xrdb.c']
deps = [
  cc.find_library('X11', required: true),
  cc.find_library('Xmu', required: true),
]

# Standard paths where the C preprocesor binary might be located
cpp_paths = [
  '/bin/cpp',
  '/usr/bin/cpp',
  '/usr/lib/cpp',
  '/usr/local/bin/cpp',
]

cpp_macro = '-DCPP='
foreach path : cpp_paths
  cpp_macro += f'"@path@",'
endforeach
add_project_arguments(cpp_macro, language: 'c')

# Check for the presence of these C stdlib functions
funcs_to_check = [
  ['asprintf', 'HAVE_ASPRINTF'],
  ['mkstemp', 'HAVE_MKSTEMP'],
  ['reallocarray', 'HAVE_REALLOCARRAY'],
]
defmacro_template = '-D@0@'

foreach fn : funcs_to_check
  if cc.has_function(fn[0])
    add_project_arguments(defmacro_template.format(fn[1]), language: 'c')
  endif
endforeach

add_project_arguments(
  '-D_DEFAULT_SOURCE', '-D_XOPEN_SOURCE=700L', f'-DPACKAGE_STRING="@package_string@"',
  language: 'c'
)
executable('xrdb', srcs, dependencies: deps)
