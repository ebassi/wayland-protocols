wayland_scanner_dep = dependency('wayland-scanner', required: false)
wayland_scanner_opt = get_option('wayland_scanner')
wayland_scanner_bin = []

# Prefer the binary passed as an option
if wayland_scanner_opt != ''
  wayland_scanner_bin += wayland_scanner_opt
endif

# Use the wayland-scanner pkg-config
if wayland_scanner_dep.found()
  wayland_scanner_bin += wayland_scanner_dep.get_pkgconfig_variable('wayland_scanner')
endif

# Fall back to the scanner in PATH
wayland_scanner_bin += 'wayland-scanner'

wayland_scanner = find_program(wayland_scanner_bin)

scan_test = find_program('scan.sh')
foreach p: protocol_files
  p_name = p[0]
  p_file = p[1]
  test('verify ' + p_name,
    scan_test,
    args: [ p_file, ],
    env: [
      'SCANNER=@0@'.format(wayland_scanner.path()),
    ],
  )
endforeach


