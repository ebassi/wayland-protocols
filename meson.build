project('wayland-protocols',
  version: '1.13',
  license: 'MIT',
  meson_version: '>= 0.45.0',
)

pkgdatadir = join_paths(get_option('datadir'), meson.project_name())

protocol_files = []

# name, [version, ...]
unstable_protocols = [
  [ 'pointer-gestures', ['v1',], ],
  [ 'fullscreen-shell', ['v1',], ],
  [ 'linux-dmabuf', ['v1',], ],
  [ 'text-input', ['v1',], ],
  [ 'input-method', ['v1',], ],
  [ 'xdg-shell', ['v5', 'v6',], ],
  [ 'relative-pointer', ['v1',], ],
  [ 'pointer-constraints', ['v1',], ],
  [ 'tablet', ['v1', 'v2',], ],
  [ 'xdg-foreign', ['v1', 'v2',], ],
  [ 'idle-inhibit', ['v1',], ],
  [ 'xwayland-keyboard-grab', ['v1',], ],
  [ 'keyboard-shortcuts-inhibit', ['v1',], ],
  [ 'xdg-output', ['v1',], ],
  [ 'input-timestamps', ['v1',], ],
]

foreach p: unstable_protocols
  p_name = p[0]
  p_versions = p[1]
  foreach version: p_versions
    xml_file = join_paths('unstable', p_name, '@0@-unstable-@1@.xml'.format(p_name, version))
    protocol_files += [[p_name, files(xml_file)]]
    install_data(xml_file, install_dir: join_paths(pkgdatadir, 'unstable', p_name))
  endforeach
endforeach

stable_protocols = [
  'presentation-time',
  'viewporter',
  'xdg-shell',
]

foreach p_name: stable_protocols
  xml_file = join_paths('stable', p_name, '@0@.xml'.format(p_name))
  protocol_files += [[p_name, files(xml_file)]]
  install_data(xml_file, install_dir: join_paths(pkgdatadir, 'stable', p_name))
endforeach

pkgconfig = import('pkgconfig')
pkgconfig.generate(
  name: meson.project_name(),
  description: 'Wayland protocol files',
  version: meson.project_version(),
  variables: [
    'datarootdir=${prefix}/@0@'.format(get_option('datadir')),
    'pkgdatadir=${pc_sysrootdir}${datarootdir}/@0@'.format(meson.project_name()),
  ],
  install_dir: join_paths(get_option('datadir'), 'pkgconfig'),
)

subdir('tests')
