marshallers = gnome.genmarshal('terminal-marshal',
sources: 'terminal-marshal.list',
install_header : true,
install_dir : get_option('includedir'),
prefix : '_terminal_marshal'
)

marshal_c = marshallers[0]
marshal_h = marshallers[1]

enums = []

enums += gnome.mkenums('types',
	sources : 'terminal-profile.h',
	c_template: 'terminal-type-builtins.c.template',
	h_template: 'terminal-type-builtins.h.template')

src = []

src += [
	'eggdesktopfile.c',
	'eggshell.c',
	'eggsmclient.c',
	'eggsmclient-xsmp.c',
	'profile-editor.c',
	'skey-popup.c',
	'terminal-accels.c',
	'terminal-app.c',
	'terminal.c',
	'terminal-close-button.c',
	'terminal-debug.c',
	'terminal-encoding.c',
	'terminal-info-bar.c',
	'terminal-options.c',
	'terminal-profile.c',
	'terminal-screen.c',
	'terminal-screen-container.c',
	'terminal-search-dialog.c',
	'terminal-tab-label.c',
	'terminal-tabs-menu.c',
	'terminal-util.c',
	'terminal-window.c',
	marshal_c,
	marshal_h,
	enums


	]

executable('mate-terminal', src, install : true, include_directories: top_inc,
	dependencies: deps, link_args: '-lm', link_with: skey,
	c_args : '-DTERMINAL_COMPILATION')

install_data(	
		'encodings-dialog.ui',
		'find-dialog.ui',
		'keybinding-editor.ui',
		'profile-manager.ui',
		'profile-new-dialog.ui',
		'profile-preferences.ui',
		'skey-challenge.ui',
		install_dir: join_paths([pkgdatadir, 'uidir']))

msgfmt = find_program('msgfmt')

conf_data = configuration_data()
conf_data.set('TERMINAL_MAJOR_VERSION','1')
conf_data.set('TERMINAL_MINOR_VERSION','9')
conf_data.set('TERMINAL_MICRO_VERSION','1')
configure_file(
	input : 'terminal-version.h.in',
	output : 'terminal-version.h',
	configuration: conf_data
)