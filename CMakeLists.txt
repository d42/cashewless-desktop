project( kde4project )
find_package( KDE4 REQUIRED )
include(KDE4Defaults)
 
include_directories( ${KDE4_INCLUDES} )
set(desktop_SRCS
    desktop.cpp
    itemspace.cpp
    desktoplayout.cpp)

set(krunner_xml org.kde.krunner.App.xml)
SET (CMAKE_CXX_COMPILER             "/usr/bin/clang++")
SET (CMAKE_CXX_FLAGS                "-Wall")
QT4_ADD_DBUS_INTERFACE(desktop_SRCS ${krunner_xml} krunner_interface)

kde4_add_plugin(plasma_containment_desktop ${desktop_SRCS})
target_link_libraries(plasma_containment_desktop ${KDE4_PLASMA_LIBS} ${KDE4_KIO_LIBS} ${KDE4_KFILE_LIBS})

install(TARGETS plasma_containment_desktop DESTINATION ${PLUGIN_INSTALL_DIR})
install(FILES plasma-containment-desktop.desktop plasma-containment-desktopdashboard.desktop  DESTINATION ${SERVICES_INSTALL_DIR})
install(FILES plasma_desktop_containment.kwinrules DESTINATION ${DATA_INSTALL_DIR}/kwin/default_rules)
