if(NOT DEFINED ENV{IDF_PATH})
  message(FATAL_ERROR "The IDF_PATH environment variable must point to the location of the ESP-IDF.")
endif()
set(INGESTION_SDK_C_DIR ingestion-sdk-c)
set(QCBOR_DIR ${INGESTION_SDK_C_DIR}/QCBOR)
set(COMPONENT_NAME ingestion-sdk-c)
#AUX_SOURCE_DIRECTORY(${QCBOR_DIR}/src SRC_FILES) 
FILE(GLOB SRC_FILES ${QCBOR_DIR}/src/*.c)

idf_component_register(
  SRCS ${SRC_FILES}
  INCLUDE_DIRS ${INGESTION_SDK_C_DIR}/inc ${INGESTION_SDK_C_DIR}/inc/signing ${QCBOR_DIR}/inc 
  REQUIRES mbedtls)
  
# Reduce the level of paranoia to be able to compile sources
target_compile_options(${COMPONENT_LIB} PRIVATE
  -Wno-maybe-uninitialized
  -Wno-missing-field-initializers
  #-Wno-type-limits
  )