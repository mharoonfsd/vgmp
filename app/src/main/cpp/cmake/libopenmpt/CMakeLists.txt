set(OPENMPT_ROOT "${CMAKE_CURRENT_SOURCE_DIR}/../../libopenmpt")

file(GLOB OPENMPT_COMMON_SOURCES CONFIGURE_DEPENDS
    "${OPENMPT_ROOT}/common/*.cpp"
)
file(GLOB OPENMPT_API_SOURCES CONFIGURE_DEPENDS
    "${OPENMPT_ROOT}/libopenmpt/*.cpp"
)
file(GLOB OPENMPT_SOUNDLIB_SOURCES CONFIGURE_DEPENDS
    "${OPENMPT_ROOT}/soundlib/*.cpp"
    "${OPENMPT_ROOT}/soundlib/plugins/*.cpp"
    "${OPENMPT_ROOT}/soundlib/plugins/dmo/*.cpp"
)
file(GLOB OPENMPT_DSP_SOURCES CONFIGURE_DEPENDS
    "${OPENMPT_ROOT}/sounddsp/*.cpp"
)

add_library(openmpt_static STATIC
    ${OPENMPT_COMMON_SOURCES}
    ${OPENMPT_API_SOURCES}
    ${OPENMPT_SOUNDLIB_SOURCES}
    ${OPENMPT_DSP_SOURCES}
)

target_include_directories(openmpt_static PUBLIC
    "${OPENMPT_ROOT}"
    "${OPENMPT_ROOT}/src"
    "${OPENMPT_ROOT}/common"
    "${OPENMPT_ROOT}/include"
)

target_compile_definitions(openmpt_static PRIVATE
    LIBOPENMPT_BUILD
    MPT_WITH_ZLIB
)

target_compile_features(openmpt_static PRIVATE cxx_std_17)
target_link_libraries(openmpt_static PUBLIC z)