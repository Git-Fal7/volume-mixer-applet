## sources
CONFIGURE_FILE(${CMAKE_CURRENT_SOURCE_DIR}/config.h.in
   ${CMAKE_CURRENT_BINARY_DIR}/config.h)
set(PNMixer_sources
	alsa.c
	audio.c
	hotkey.c
	hotkeys.c
	main.c
	notif.c
	prefs.c
	support-intl.c
	support-log.c
	support-ui.c
	ui-about-dialog.c
	ui-hotkey-dialog.c
	ui-popup-menu.c
	ui-popup-window.c
	ui-prefs-dialog.c
	ui-tray-icon.c
)


## includes
include_directories(
	"${CMAKE_CURRENT_BINARY_DIR}"
)


## libraries
set(default_deps
   	alsa
	glib-2.0
	x11
	gtk+-3.0>=3.12.0
)

pkg_check_modules(PNMixer_DEPS REQUIRED
	${default_deps}
)


## main pnmixer target
add_executable(volume-mixer-applet ${PNMixer_sources})
# and its flags
target_link_libraries(volume-mixer-applet "${PNMixer_DEPS_LDFLAGS}")
target_link_libraries(volume-mixer-applet m)
target_compile_options(volume-mixer-applet PUBLIC "${PNMixer_DEPS_CFLAGS}")
target_compile_definitions(volume-mixer-applet PUBLIC -DHAVE_CONFIG_H)

install(TARGETS volume-mixer-applet DESTINATION "${CMAKE_INSTALL_BINDIR}")
