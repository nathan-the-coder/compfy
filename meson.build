project('compfy', 'c', version: '1.7.2',
        default_options: ['c_std=c11', 'warning_level=1', 'buildtype=release'])

cc = meson.get_compiler('c')

# use project version by default
version = 'v'+meson.project_version()

add_project_arguments('-fno-lto', language : 'c')

add_global_arguments('-DCOMPFY_VERSION="'+version+'"', language: 'c')

if get_option('buildtype') == 'release'
	add_global_arguments('-DNDEBUG', language: 'c')
endif

add_global_arguments('-D_GNU_SOURCE', language: 'c')

if cc.has_header('stdc-predef.h')
	add_global_arguments('-DHAS_STDC_PREDEF_H', language: 'c')
endif

if get_option('warning_level') != '0'
  warns = [ 'cast-function-type', 'ignored-qualifiers', 'missing-parameter-type',
            'nonnull', 'shadow', 'no-type-limits', 'old-style-declaration', 'override-init',
            'sign-compare', 'type-limits', 'uninitialized', 'shift-negative-value',
            'unused-but-set-parameter', 'unused-parameter', 'implicit-fallthrough=2',
            'no-unknown-warning-option', 'no-missing-braces', 'conversion', 'empty-body' ]
  foreach w : warns
          if cc.has_argument('-W'+w)
                  add_global_arguments('-W'+w, language: 'c')
          endif
  endforeach
endif

if get_option('with_docs')
	install_data('./man/compfy.1', install_dir: join_paths(get_option('mandir'), 'man1'))
endif

subdir('src')

install_data('compfy.desktop', install_dir: 'share/applications')
install_data('compfy.desktop', install_dir: get_option('sysconfdir') / 'xdg' / 'autostart')
install_data('media/compfy.svg', install_dir: 'share/icons/hicolor/scalable/apps')
install_data('media/icons/compfy.png', install_dir: 'share/icons/hicolor/48x48/apps')
