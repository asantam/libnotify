project('libnotify',
  'c',
  version: '0.7.8',
  meson_version: '>= 0.47.0')

gnome = import('gnome')
pkgconfig = import('pkgconfig')

################################################################
# libtool versioning
################################################################
#
# +1 :  0 : +1   == new interface that does not break old one.
# +1 :  0 :  0   == removed an interface. Breaks old apps.
#  ? : +1 :  ?   == internal changes that doesn't break anything.
#
# CURRENT : REVISION : AGE
#
LT_CURRENT=4
LT_REVISION=0
LT_AGE=0

VERSION_ARRAY = meson.project_version().split('.')
MODULE_VERSION = '@0@.@1@'.format(VERSION_ARRAY[0], VERSION_ARRAY[1])
LIBNAME = meson.project_name().split('lib')[1]

default_includes = include_directories('.')

prefix = get_option('prefix')
includedir = join_paths(prefix, get_option('includedir'))
docdir = join_paths(prefix, get_option('datadir'), 'doc', meson.project_name())

libnotify_deps = []
extra_deps = []

glib_req_version = '>= 2.26.0'

gdk_pixbuf_dep = dependency('gdk-pixbuf-2.0')
glib_dep = dependency('glib-2.0', version: glib_req_version)
gio_dep = dependency('gio-2.0', version: glib_req_version)
gtk_dep = dependency('gtk+-3.0', version: '>= 2.90', required: get_option('tests'))

libnotify_deps = [gdk_pixbuf_dep, gio_dep, glib_dep]
tests_deps = [gtk_dep]

conf = configuration_data()
conf.set_quoted('VERSION', meson.project_version())
configure_file(input: 'config.h.meson',
  output : 'config.h',
  configuration : conf)

subdir('libnotify')
subdir('tools')
subdir('docs')

if get_option('tests')
  subdir('tests')
endif
