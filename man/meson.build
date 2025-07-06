sed = find_program('sed')
xrdb_version = 'xrdb @0@'.format(meson.project_version())

custom_target(
  'xrdb.man',
  input: 'xrdb.man',
  output: 'xrdb.1',
  capture: true,
  install: true,
  install_dir: '.',
  command: [
    sed,
    '-e', f's/__xorgversion__/"@xrdb_version@" "X Version 11"/g',
    '@INPUT@'
  ],
)
