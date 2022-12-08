if(CUSTOM_EXT2FS)
  find_package(ext2fs REQUIRED)
  include_directories(${EXT2FS_INCLUDE_DIR})
  set(LIB_EXT2FS ${EXT2FS_LIBRARY})
else()
  set(LIB_EXT2FS ext2fs)
endif()

add_library(extfs_lib
  extfs_io.cpp
  extfs.cpp
)
target_include_directories(extfs_lib PUBLIC
  ${PHOTON_INCLUDE_DIR}
)
target_link_libraries(extfs_lib
  photon_static
  overlaybd_lib
  ${LIB_EXT2FS}
)

if(BUILD_TESTING)
  add_subdirectory(test)
endif()