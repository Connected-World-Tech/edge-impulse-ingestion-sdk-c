if(NOT DEFINED ENV{IDF_PATH})
  message(FATAL_ERROR "The IDF_PATH environment variable must point to the location of the ESP-IDF.")
endif()
set(QCBOR_DIR ingestion-sdk-c/QCBOR)
AUX_SOURCE_DIRECTORY(${QCBOR_DIR}/src SRC_FILES) 
idf_component_register(
  SRCS ${SRC_FILES}
  INCLUDE_DIRS inc inc/signing ${QCBOR_DIR}/inc)