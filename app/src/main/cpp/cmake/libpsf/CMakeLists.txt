set(PSF_ROOT "${CMAKE_CURRENT_SOURCE_DIR}/../../libpsf")

add_library(psf STATIC
    "${PSF_ROOT}/PsxBios.c"
    "${PSF_ROOT}/PsxCounters.c"
    "${PSF_ROOT}/PsxDma.c"
    "${PSF_ROOT}/Spu.c"
    "${PSF_ROOT}/PsxHw.c"
    "${PSF_ROOT}/PsxMem.c"
    "${PSF_ROOT}/Misc.c"
    "${PSF_ROOT}/R3000A.c"
    "${PSF_ROOT}/PsxInterpreter.c"
    "${PSF_ROOT}/PsxHLE.c"
    "${PSF_ROOT}/spu/spu.c"
)

target_include_directories(psf PUBLIC
    "${PSF_ROOT}"
    "${PSF_ROOT}/spu"
)

target_compile_definitions(psf PRIVATE
    PSS_STYLE=1
    SPSFVERSION=\"0.4.8\"
)

target_compile_options(psf PRIVATE -fPIC)
target_link_libraries(psf PUBLIC z)