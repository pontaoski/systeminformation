project('me.Appadeia.systeminformation', ['vala', 'c'],
    version : '1.0.0',
    license: 'GPL-3.0'
)

add_project_arguments([
        '-DGETTEXT_PACKAGE="@0@"'.format(meson.project_name())
    ],
    language: 'c',
)

gnome = import('gnome')
i18n = import('i18n')

gresource = gnome.compile_resources(
    'as-resources', 'data/me.Appadeia.systeminformation.gresource.xml',
    source_dir: 'data',
    c_name: 'as'
)

conf = configuration_data()
conf.set_quoted('GETTEXT_PACKAGE', meson.project_name())
configure_file(output: 'config.h', configuration: conf)
config_h_dir = include_directories('.')

c_args = [
  '-include', 'config.h',
  '-DHANDY_USE_UNSTABLE_API'
]

sources = files()

subdir('data')
subdir('po')
subdir('src')
subdir('tests')

dependencies = [
	dependency('gobject-2.0'),
    dependency('glib-2.0'),
    dependency('gtk+-3.0'),
    dependency('libhandy-0.0'),
    dependency('gee-0.8'),
    meson.get_compiler('vala').find_library('posix'),
]

e = executable('me.Appadeia.systeminformation',
    sources,
    gresource,
    c_args: c_args,
    dependencies: dependencies,
    install : true
)

#test('tests', e, args : ['--run-tests'])

meson.add_install_script('meson/post_install.py')
