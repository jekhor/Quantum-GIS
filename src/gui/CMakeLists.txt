
SET(QGIS_GUI_SRCS

symbology-ng/qgsbrushstylecombobox.cpp
symbology-ng/qgscolorrampcombobox.cpp
symbology-ng/qgsdashspacedialog.cpp
symbology-ng/qgspenstylecombobox.cpp
symbology-ng/qgssymbollayerv2widget.cpp
symbology-ng/qgssymbolv2propertiesdialog.cpp
symbology-ng/qgsrendererv2widget.cpp
symbology-ng/qgssinglesymbolrendererv2widget.cpp
symbology-ng/qgscategorizedsymbolrendererv2widget.cpp
symbology-ng/qgsgraduatedsymbolrendererv2widget.cpp
symbology-ng/qgsrulebasedrendererv2widget.cpp
symbology-ng/qgsrendererv2propertiesdialog.cpp
symbology-ng/qgsstylev2managerdialog.cpp
symbology-ng/qgssymbollevelsv2dialog.cpp
symbology-ng/qgssymbolv2selectordialog.cpp
symbology-ng/qgsvectorgradientcolorrampv2dialog.cpp
symbology-ng/qgsvectorrandomcolorrampv2dialog.cpp
symbology-ng/qgsvectorcolorbrewercolorrampv2dialog.cpp
symbology-ng/characterwidget.cpp
symbology-ng/qgsstylev2exportimportdialog.cpp

attributetable/qgsattributetablemodel.cpp
attributetable/qgsattributetablememorymodel.cpp
attributetable/qgsattributetableview.cpp
attributetable/qgsattributetablefiltermodel.cpp
attributetable/qgsattributetableidcolumnpair.cpp
attributetable/qgsattributetabledelegate.cpp

qgisgui.cpp
qgisinterface.cpp
qgsannotationitem.cpp
qgsattributeeditor.cpp
qgslegendinterface.cpp
qgscolorbutton.cpp
qgscomposerview.cpp
qgscursors.cpp
qgsdetaileditemdelegate.cpp
qgsdetaileditemwidget.cpp
qgsdetaileditemdata.cpp
qgsencodingfiledialog.cpp
qgsfiledropedit.cpp
qgsfieldvalidator.cpp
qgsformannotationitem.cpp
qgsgenericprojectionselector.cpp
qgsmanageconnectionsdialog.cpp
qgsmapcanvas.cpp
qgsmapcanvasitem.cpp
qgsmapcanvasmap.cpp
qgsmapcanvassnapper.cpp
qgsmapoverviewcanvas.cpp
qgsmaptip.cpp
qgsmaptool.cpp
qgsmaptoolemitpoint.cpp
qgsmaptoolpan.cpp
qgsmaptoolzoom.cpp
qgsmessageviewer.cpp
qgsnewhttpconnection.cpp
qgsnewvectorlayerdialog.cpp
qgsnumericsortlistviewitem.cpp
qgscredentialdialog.cpp
qgsprojectbadlayerguihandler.cpp
qgsprojectionselector.cpp
qgsquickprint.cpp
qgsrubberband.cpp
qgstextannotationitem.cpp
qgsvertexmarker.cpp
qgsludialog.cpp
qgssearchquerybuilder.cpp
)

SET(QGIS_GUI_MOC_HDRS

symbology-ng/qgsdashspacedialog.h
symbology-ng/qgssymbollayerv2widget.h
symbology-ng/qgssymbolv2propertiesdialog.h
symbology-ng/qgssinglesymbolrendererv2widget.h
symbology-ng/qgscategorizedsymbolrendererv2widget.h
symbology-ng/qgsgraduatedsymbolrendererv2widget.h
symbology-ng/qgsrulebasedrendererv2widget.h
symbology-ng/qgsrendererv2widget.h
symbology-ng/qgsrendererv2propertiesdialog.h
symbology-ng/qgsstylev2managerdialog.h
symbology-ng/qgssymbollevelsv2dialog.h
symbology-ng/qgssymbolv2selectordialog.h
symbology-ng/qgsvectorgradientcolorrampv2dialog.h
symbology-ng/qgsvectorrandomcolorrampv2dialog.h
symbology-ng/qgsvectorcolorbrewercolorrampv2dialog.h
symbology-ng/qgscolorrampcombobox.h
symbology-ng/characterwidget.h
symbology-ng/qgspenstylecombobox.h
symbology-ng/qgsbrushstylecombobox.h
symbology-ng/qgsstylev2exportimportdialog.h

attributetable/qgsattributetableview.h
attributetable/qgsattributetablemodel.h
attributetable/qgsattributetablememorymodel.h
attributetable/qgsattributetabledelegate.h

qgsattributeeditor.h
qgscomposerview.h
qgsdetaileditemdelegate.h
qgsdetaileditemwidget.h
qgslegendinterface.h
qgisinterface.h
qgsencodingfiledialog.h
qgsfieldvalidator.h
qgsformannotationitem.h
qgsgenericprojectionselector.h
qgsmanageconnectionsdialog.h
qgsmapcanvas.h
qgsmapoverviewcanvas.h
qgsmaptoolemitpoint.h
qgsmessageviewer.h
qgsnewhttpconnection.h
qgsnewvectorlayerdialog.h
qgscredentialdialog.h
qgsprojectionselector.h
qgsquickprint.h
qgsludialog.h
qgsprojectbadlayerguihandler.h
qgslonglongvalidator.h
qgssearchquerybuilder.h
)

QT4_WRAP_CPP(QGIS_GUI_MOC_SRCS ${QGIS_GUI_MOC_HDRS})


INCLUDE_DIRECTORIES(
  ${QT_QTUITOOLS_INCLUDE_DIR}
  ${CMAKE_CURRENT_SOURCE_DIR}
  ${CMAKE_CURRENT_SOURCE_DIR}/symbology-ng
  ../core
  ../core/composer
  ../core/raster
  ../core/renderer
  ../core/symbology
  ../core/symbology-ng
  ${CMAKE_CURRENT_BINARY_DIR}
  ${CMAKE_CURRENT_BINARY_DIR}/../ui
)
IF (WITH_INTERNAL_SPATIALITE)
  INCLUDE_DIRECTORIES(../core/spatialite/headers)
  INCLUDE_DIRECTORIES(../core/spatialite/headers/spatialite)
ELSE (WITH_INTERNAL_SPATIALITE)
  INCLUDE_DIRECTORIES(${SQLITE3_INCLUDE_DIR})
ENDIF (WITH_INTERNAL_SPATIALITE)

INCLUDE_DIRECTORIES(${GEOS_INCLUDE_DIR})

IF (WIN32)
  IF (MSVC)
    ADD_DEFINITIONS("-DGUI_EXPORT=__declspec(dllexport)")
  ELSE (MSVC)
    ADD_DEFINITIONS("-UGUI_EXPORT \"-DGUI_EXPORT=__declspec(dllexport)\"")
  ENDIF (MSVC)
ENDIF (WIN32)

# disable deprecation warnings for classes re-exporting deprecated methods
IF(MSVC)
  SET_SOURCE_FILES_PROPERTIES(
    ${CMAKE_BINARY_DIR}/src/gui/moc_qgisinterface.cxx
    ${CMAKE_BINARY_DIR}/src/gui/moc_qgsgenericprojectionselector.cxx
    ${CMAKE_BINARY_DIR}/src/gui/moc_qgsprojectionselector.cxx
    PROPERTIES COMPILE_FLAGS "-wd4996")
ELSE(MSVC)
  SET_SOURCE_FILES_PROPERTIES(
    ${CMAKE_BINARY_DIR}/src/gui/moc_qgisinterface.cxx
    ${CMAKE_BINARY_DIR}/src/gui/moc_qgsgenericprojectionselector.cxx
    ${CMAKE_BINARY_DIR}/src/gui/moc_qgsprojectionselector.cxx
    PROPERTIES COMPILE_FLAGS "-w")
ENDIF(MSVC)

#############################################################
# qgis_gui library

ADD_LIBRARY(qgis_gui SHARED ${QGIS_GUI_SRCS} ${QGIS_GUI_MOC_SRCS})

SET_TARGET_PROPERTIES(qgis_gui PROPERTIES VERSION ${COMPLETE_VERSION} SOVERSION ${COMPLETE_VERSION})

# make sure that UI files will be processed first
ADD_DEPENDENCIES(qgis_gui ui)

TARGET_LINK_LIBRARIES(qgis_gui
  qgis_core
  ${QT_QTUITOOLS_LIBRARY}
)

IF (NOT WITH_INTERNAL_SPATIALITE)
  TARGET_LINK_LIBRARIES(qgis_gui ${SQLITE3_LIBRARIES})
ENDIF (NOT WITH_INTERNAL_SPATIALITE)

IF (APPLE)
  SET_TARGET_PROPERTIES(qgis_gui PROPERTIES BUILD_WITH_INSTALL_RPATH TRUE )
ENDIF (APPLE)

INSTALL(TARGETS qgis_gui
  RUNTIME DESTINATION ${QGIS_BIN_DIR}
  LIBRARY DESTINATION ${QGIS_LIB_DIR}
  ARCHIVE DESTINATION ${QGIS_LIB_DIR})

# for installing headers

SET(QGIS_GUI_HDRS
qgisgui.h
qgisinterface.h
qgscolorbutton.h
qgscursors.h
qgsencodingfiledialog.h
qgsfiledropedit.h
qgsgenericprojectionselector.h
qgsmapcanvas.h
qgsmapcanvasitem.h
qgsmapcanvasmap.h
qgsmapcanvassnapper.h
qgsmapoverviewcanvas.h
qgsmaptool.h
qgsmaptoolemitpoint.h
qgsmaptoolpan.h
qgsmaptoolzoom.h
qgsmessageviewer.h
qgscredentialdialog.h
qgsprojectionselector.h
qgsrubberband.h
qgsvertexmarker.h
qgsmaptip.h
qgssearchquerybuilder.h
qgsattributeeditor.h
qgsfieldvalidator.h

attributetable/qgsattributetablemodel.h
attributetable/qgsattributetablememorymodel.h
attributetable/qgsattributetableview.h
attributetable/qgsattributetablefiltermodel.h
attributetable/qgsattributetableidcolumnpair.h
attributetable/qgsattributetabledelegate.h

${CMAKE_CURRENT_BINARY_DIR}/../ui/ui_qgsdetaileditemwidgetbase.h
${CMAKE_CURRENT_BINARY_DIR}/../ui/ui_qgsgenericprojectionselectorbase.h
${CMAKE_CURRENT_BINARY_DIR}/../ui/ui_qgsmessageviewer.h
${CMAKE_CURRENT_BINARY_DIR}/../ui/ui_qgscredentialdialog.h
${CMAKE_CURRENT_BINARY_DIR}/../ui/ui_qgsprojectionselectorbase.h
${CMAKE_CURRENT_BINARY_DIR}/../ui/ui_qgsquerybuilderbase.h
)


INSTALL(CODE "MESSAGE(\"Installing GUI headers...\")")
INSTALL(FILES ${QGIS_GUI_HDRS} ${QGIS_GUI_MOC_HDRS} DESTINATION ${QGIS_INCLUDE_DIR})

