file(GLOB ui_files *.glade)

install(FILES ${ui_files} DESTINATION "${CMAKE_INSTALL_DATADIR}/${PACKAGE}/ui")


## make running 'src/pnmixer' from the build directory work
## since pnmixer looks up ui files from a relative path
symlink_to_binary_dir("${ui_files}")

