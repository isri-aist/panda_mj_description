# Panda_mj_description

This repository contains the panda model for [mc_mujoco](https://github.com/rohanpsingh/mc_mujoco).

The package will install the files in this directory so that mc_mujoco can pick them up automatically.

Please note that only **Panda (PandaDefault)**, **PandaHand** are supported.

## Requirement 

Please make sure [mc_mujoco](https://github.com/rohanpsingh/mc_mujoco) is installed. 

## Install

### From source 

In order to install from source please run the following commands : 

```bash
git clone https://github.com/isri-aist/panda_mj_description
cd panda_mj_description
mkdir build && cd build
cmake ..
make install
```


## To run 

Your mc_rtc configuration file (typically ~/.config/mc_rtc/mc_rtc.yaml) should contain the following lines:

```yaml
# General mc_rtc configuration to run a panda controller at 1kHz
MainRobot: PandaDefault # Or PandaHand according to the end-effector installed on the robot
Enabled: Posture # Edit with your controller
Timestep: 0.001
```
Then run mc_mujoco

```bash
mc_mujoco
```

## Add your model

In order to add your model, you need to :

1. Add your mesh files in the `/meshes` folder 
2. Add your xml model to `/xml` folder
3. Add a folder to pdgains with the name of your model, create a file `PDgains_sim.dat` inside of it.
4. Update models list in `CMakeLists.txt` 
5. Then install `make install` or `ninja install`

### Acknowledgement 

* [google-deepmind](https://github.com/google-deepmind/mujoco_menagerie/tree/main/franka_emika_panda)q