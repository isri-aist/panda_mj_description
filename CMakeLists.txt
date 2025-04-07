cmake_minimum_required(VERSION 3.10)

project(panda_mj_description VERSION 1.0.0)

if(NOT TARGET mc_mujoco)
  find_package(mc_mujoco REQUIRED)
endif()

option(SRC_MODE "Use files in the repository instead of installed files" OFF)

# Supported panda models
set(panda_models
    panda_default
    panda_hand
)

foreach(MODEL IN LISTS panda_models)
    if(SRC_MODE)
        set(PANDA_XML_MODEL_PATH "${CMAKE_CURRENT_SOURCE_DIR}/xml/${MODEL}.xml")
        set(PANDA_PDGAINS_PATH "${CMAKE_CURRENT_SOURCE_DIR}/pdgains/${MODEL}/PDgains_sim.dat")
    else()
        set(PANDA_XML_MODEL_PATH "${MC_MUJOCO_SHARE_DESTINATION}/panda/xml/${MODEL}.xml")
        set(PANDA_PDGAINS_PATH "${MC_MUJOCO_SHARE_DESTINATION}/panda/pdgains/${MODEL}/PDgains_sim.dat")
    endif()

    configure_file(mc_mujoco/panda.in.yaml "${CMAKE_CURRENT_BINARY_DIR}/mc_mujoco/${MODEL}.yaml")
    install(FILES "${CMAKE_CURRENT_BINARY_DIR}/mc_mujoco/${MODEL}.yaml" DESTINATION "${MC_MUJOCO_SHARE_DESTINATION}")
    install(DIRECTORY pdgains DESTINATION "${MC_MUJOCO_SHARE_DESTINATION}/panda")

endforeach()

install(DIRECTORY meshes DESTINATION "${MC_MUJOCO_SHARE_DESTINATION}/panda")
install(DIRECTORY xml DESTINATION "${MC_MUJOCO_SHARE_DESTINATION}/panda" FILES_MATCHING PATTERN "*.xml")