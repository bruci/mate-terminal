project('mate-terminal','c', version: '1.19.0', meson_version: '>=0.36.0')

i18n = import('i18n')
gnome = import('gnome')

conf = configuration_data()

top_inc = include_directories('.')

deps = [ dependency('gtk+-3.0', version : '>=3.22'),
	dependency('libxml-2.0'),
	dependency('gmodule-2.0'),
	dependency('glib-2.0'),
  dependency('vte-2.91'),
  dependency('dconf'),
  dependency('x11'),
  dependency('gio-2.0'),
  dependency('gthread-2.0'),
  dependency('sm'),
  dependency('ice')
  ]

datadir = join_paths([ get_option('prefix'),
                       get_option('datadir') ])
pkgdatadir = join_paths([ get_option('prefix'),
                          get_option('datadir'),
                          'mate-terminal' ])
bindir = join_paths([ get_option('prefix'), 'bin' ])
schemadir = join_paths([ datadir, 'glib-2.0', 'schemas' ])

conf.set('G_LOG_USE_STRUCTURED', true)
conf.set_quoted('G_LOG_DOMAIN', 'org.mate.terminal')
conf.set_quoted('PACKAGE', 'mate-terminal')
conf.set_quoted('PACKAGE_NAME', 'mate-terminal')
conf.set_quoted('EXECUTABLE_NAME', 'mate-terminal')
conf.set_quoted('PACKAGE_VERSION', meson.project_version())
conf.set_quoted('PACKAGE_STRING', 'oh_fuck_you')
conf.set_quoted('VERSION', meson.project_version())
conf.set_quoted('GETTEXT_PACKAGE', 'mate-terminal')
conf.set_quoted('TERM_DATADIR', datadir)
conf.set_quoted('UI_DIR', join_paths([pkgdatadir,'uidir']))
conf.set_quoted('TERM_PKGDATADIR', pkgdatadir)
conf.set_quoted('TERM_LOCALEDIR', join_paths([ get_option('prefix'),
                                          get_option('datadir'),
                                          'locale' ]))

conf.set_quoted('pkgdatadir', pkgdatadir)
conf.set_quoted('bindir', bindir)

configure_file(output : 'config.h', configuration : conf)

msgfmt = find_program('msgfmt')

custom_target('desktop-file',
              output: 'mate-terminal.desktop',
              input: files('mate-terminal.desktop.in.in'),
              install: true,
              install_dir: join_paths([datadir,'applications']),
              command: [msgfmt, '--desktop', '-d', '../po', '--template', '@INPUT@', '-o', '@OUTPUT@'])

custom_target('appdata',
              output: 'mate-terminal.appdata.xml',
              input: files('mate-terminal.appdata.xml.in'),
              install: true,
              install_dir: join_paths([datadir,'appdata']),
              command: [msgfmt, '--xml', '-d', '../po', '--template', '@INPUT@', '-o', '@OUTPUT@'])

subdir('src/skey')
subdir('src')
subdir('po')
#subdir('help') not ready
