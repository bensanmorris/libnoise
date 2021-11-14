set(PROJECT_NAME libnoise)
include_directories (noise)
set(libSrcs ${libSrcs}
    noisegen.cpp
    latlon.cpp
    model/line.cpp
    model/plane.cpp
    model/sphere.cpp
    model/cylinder.cpp
    module/abs.cpp
    module/add.cpp
    module/billow.cpp
    module/blend.cpp
    module/cache.cpp
    module/checkerboard.cpp
    module/clamp.cpp
    module/const.cpp
    module/curve.cpp
    module/cylinders.cpp
    module/displace.cpp
    module/exponent.cpp
    module/invert.cpp
    module/max.cpp
    module/min.cpp
    module/modulebase.cpp
    module/multiply.cpp
    module/perlin.cpp
    module/power.cpp
    module/ridgedmulti.cpp
    module/rotatepoint.cpp
    module/scalebias.cpp
    module/scalepoint.cpp
    module/select.cpp
    module/spheres.cpp
    module/terrace.cpp
    module/translatepoint.cpp
    module/turbulence.cpp
    module/voronoi.cpp
)
if(BUILD_SHARED_LIBS)
    if(WIN32)
		add_library(noise SHARED ${libSrcs} win32/dllmain.cpp)
    else()
		add_library(noise SHARED ${libSrcs})
    endif()
	set_target_properties(noise PROPERTIES LIBNOISE_VERSION ${LIBNOISE_VERSION})
	target_compile_definitions(noise PRIVATE NOISE_BUILD_DLL)
	install(TARGETS noise DESTINATION "${CMAKE_INSTALL_PREFIX}/bin")
else()
	add_library(noise-static STATIC ${libSrcs})
	set_target_properties(noise-static PROPERTIES LIBNOISE_VERSION ${LIBNOISE_VERSION})
	target_compile_definitions(noise-static PUBLIC NOISE_STATIC)
	install(TARGETS noise-static DESTINATION "${CMAKE_INSTALL_PREFIX}/lib")
endif()
install(DIRECTORY "${PROJECT_SOURCE_DIR}/src/noise" DESTINATION "${CMAKE_INSTALL_PREFIX}/include")
