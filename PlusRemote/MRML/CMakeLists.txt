project(vtkSlicer${MODULE_NAME}ModuleMRML)

set(KIT ${PROJECT_NAME})

set(${KIT}_EXPORT_DIRECTIVE "VTK_SLICER_${MODULE_NAME_UPPER}_MODULE_MRML_EXPORT")

set(${KIT}_INCLUDE_DIRECTORIES
  ${vtkSlicerOpenIGTLinkIFModuleMRML_INCLUDE_DIRS}
  ${Slicer_Base_INCLUDE_DIRS}
  ${Slicer_INSTALL_QTLOADABLEMODULES_INCLUDE_DIR}/vtkSlicerAnnotationsModuleMRML
  ${Slicer_INSTALL_QTLOADABLEMODULES_INCLUDE_DIR}/vtkSlicerMarkupsModuleMRML
  )

if (Slicer_VERSION VERSION_LESS "4.11.0")
  #TODO: When the stable version of Slicer includes the Texts module/widgets, they can be removed from SlicerOpenIGTLink
  list(APPEND ${KIT}_INCLUDE_DIRECTORIES
    ${vtkSlicerOpenIGTLinkIFModuleMRML_SOURCE_DIR}/Text
    )
endif()

set(${KIT}_SRCS
  vtkMRMLPlusRemoteNode.cxx
  vtkMRMLPlusRemoteNode.h
  vtkMRMLPlusServerNode.cxx
  vtkMRMLPlusServerNode.h
  vtkMRMLPlusServerLauncherNode.cxx
  vtkMRMLPlusServerLauncherNode.h
  vtkSlicerPlusOpenIGTLinkCommand.cxx
  vtkSlicerPlusOpenIGTLinkCommand.h
  )

set(${KIT}_TARGET_LIBRARIES
  vtkSlicerOpenIGTLinkIFModuleMRML
  )

link_directories(${Slicer_INSTALL_QTLOADABLEMODULES_LIB_DIR})

# --------------------------------------------------------------------------
SlicerMacroBuildModuleMRML(
  NAME ${KIT}
  EXPORT_DIRECTIVE ${${KIT}_EXPORT_DIRECTIVE}
  INCLUDE_DIRECTORIES ${${KIT}_INCLUDE_DIRECTORIES}
  SRCS ${${KIT}_SRCS}
  TARGET_LIBRARIES ${${KIT}_TARGET_LIBRARIES}
  )
