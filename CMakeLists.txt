cmake_minimum_required(VERSION 3.8)

project(3dtiAudioToolkit LANGUAGES CXX)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_MODULE_PATH ${CMAKE_CURRENT_LIST_DIR}/cmake/modules)

#set (NETCDF_CXX "YES")
#find_package(NetCDF REQUIRED)
#set(NETCDF_CXX_LIB NETCDF_LIBRARIES)
#find_package(sofacoustic REQUIRED)
find_package(Eigen3 REQUIRED)
find_package(cereal REQUIRED)

add_library(${PROJECT_NAME})
add_library(${PROJECT_NAME}::${PROJECT_NAME} ALIAS ${PROJECT_NAME})
target_sources(${PROJECT_NAME}
        PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/BinauralSpatializer/Environment.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/BinauralSpatializer/Core.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/BinauralSpatializer/SingleSourceDSP.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/BinauralSpatializer/BRIR.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/BinauralSpatializer/ILD.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/BinauralSpatializer/HRTF.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/BinauralSpatializer/UPCAnechoic.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/BinauralSpatializer/Listener.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/HAHLSimulation/BaerMooreFrequencySmearing.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/HAHLSimulation/HighOrderButteworthFilter.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/HAHLSimulation/HearingLossSim.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/HAHLSimulation/ClassificationScaleHL.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/HAHLSimulation/HearingAidSim.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/HAHLSimulation/GammatoneMultibandExpander.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/HAHLSimulation/Graf3DTIFrequencySmearing.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/HAHLSimulation/TemporalDistortionSimulator.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/HAHLSimulation/Fig6Algorithm.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/HAHLSimulation/DynamicEqualizer.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/HAHLSimulation/ButterworthMultibandExpander.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/Common/UPCEnvironment.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/Common/BiquadFilter.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/Common/DynamicExpanderMono.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/Common/DistanceAttenuator.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/Common/ErrorHandler.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/Common/DynamicCompressorStereo.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/Common/Vector3.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/Common/Profiler.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/Common/FiltersChain.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/Common/GammatoneFilterBank.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/Common/DynamicCompressorMono.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/Common/Transform.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/Common/fftsg.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/Common/FiltersBank.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/Common/Fprocessor.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/Common/Quaternion.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/Common/Delay.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/Common/Magnitudes.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/Common/FarDistanceEffects.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/Common/NoiseGenerator.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/Common/GammatoneFilter.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit/Common/EnvelopeDetector.cpp

        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_ResourceManager/BRIR/BRIRCereal.cpp
        #${CMAKE_CURRENT_SOURCE_DIR}/3dti_ResourceManager/BRIR/BRIRFactory.cpp
        #${CMAKE_CURRENT_SOURCE_DIR}/3dti_ResourceManager/HRTF/HRTFFactory.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_ResourceManager/HRTF/HRTFCereal.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_ResourceManager/ILD/ILDCereal.cpp
        )

target_include_directories(${PROJECT_NAME}
        PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_ResourceManager
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_ResourceManager/third_party_libraries
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_Toolkit
        ${CMAKE_CURRENT_SOURCE_DIR}/3dti_ResourceManager/third_party_libraries/sofacoustics/libsofa/src
        ${EIGEN3_INCLUDE_DIR}
        ${NETCDF_INCLUDES}
        )
target_link_libraries(${PROJECT_NAME}
        PUBLIC
        cereal
        ${Eigen_BINARY_DIR}
        ${NETCDF_LIBRARIES}
        )