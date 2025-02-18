# Copyright (C) 2023 Alessandro Iepure
#
# SPDX-License-Identifier: GPL-3.0-or-later

pkgdatadir = join_paths(get_option('prefix'), get_option('datadir'), meson.project_name())
moduledir = join_paths(pkgdatadir, 'src')
gnome = import('gnome')

# Compile resources
blueprints = custom_target('blueprints',
  input: files(
    'ui/gtk/help-overlay.blp',
    'ui/window.blp',
    'ui/about_window.blp',
    'ui/preferences.blp',

    'ui/views/main_view.blp',
    'ui/views/first_run_view.blp',
    'ui/views/content_view.blp',

    'ui/dialogs/add_manual.blp',
    'ui/dialogs/add_tmdb.blp',
    'ui/dialogs/edit_season.blp',
    'ui/dialogs/message_dialogs.blp',

    'ui/pages/edit_episode_page.blp',
    'ui/pages/details_page.blp',

    'ui/widgets/theme_switcher.blp',
    'ui/widgets/poster_button.blp',
    'ui/widgets/search_result_row.blp',
    'ui/widgets/episode_row.blp',
    'ui/widgets/image_selector.blp',
    'ui/widgets/season_expander.blp',
    'ui/widgets/background_indicator.blp',
    'ui/widgets/background_activity_row.blp',
  ),
  output: '.',
  command: [find_program('blueprint-compiler'), 'batch-compile', '@OUTPUT@', '@CURRENT_SOURCE_DIR@', '@INPUT@']
)

gnome.compile_resources('ticketbooth',
  configure_file(
    input: 'ticketbooth.gresource.xml.in',
    output: 'ticketbooth.gresource.xml',
    configuration: conf
  ),
  gresource_bundle: true,
  install: true,
  install_dir: pkgdatadir,
  dependencies: blueprints,
)

configure_file(
  input: 'ticketbooth.in',
  output: 'ticketbooth',
  configuration: conf,
  install: true,
  install_dir: get_option('bindir')
)

subdir('widgets')
subdir('dialogs')
subdir('providers')
subdir('models')
subdir('views')
subdir('pages')

# Install sources
ticketbooth_sources = [
  '__init__.py',
  'main.py',
  'window.py',
  configure_file(
    input: 'shared.py.in',
    output: 'shared.py',
    configuration: conf
  ),
  'preferences.py',
  'background_queue.py',
]

install_data(ticketbooth_sources, install_dir: moduledir)
