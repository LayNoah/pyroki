# Install ROS2
## 1. For Ubuntu 22.04, install ROS2 Humble
- Follow https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debs.html

## 2. For Ubuntu 24.04, isntall ROS2 Jazzy
- Follow https://docs.ros.org/en/jazzy/Installation/Ubuntu-Install-Debs.html

# Set .bashrc configuration
- Enter the below configuration.
```bash
sudo apt-get install vim
vi ~/.bashrc
```

- Copy and paste these commands at the end of the `~/.bashrc`
```bash
export ROS_DOMAIN_ID=34                         #use any number
export ROS_DISTRO=jazzy                         #support {jazzy, humble}
source /opt/ros/$ROS_DISTRO/setup.bash
source ~/workspaces/movensys_ws/install/setup.bash
alias pyr='env -u PYTHONPATH JAX_PLATFORMS=cpu ~/venvs/pyroki/bin/python'
```

- Open the new terminal and check the ros2 is installed or not.
```bash
ros2 topic list
```


# Install Pyroki in user workspace
```bash
source ~/.bashrc
mkdir ~/workspace/movensys_ws/src
cd ~/workspace/movensys_ws/src
git clone https://github.com/LayNoah/pyroki.git
```

# Colcon the repo
```bash
cd ~/workspaces/movensys_ws
colcon build
source ~/.bashrc
```

# Regenerate urdf files
```bash
cd ~/workspaces/movensys_ws/src/pyroki/urdf/indy_description/urdf
bash generate_all_urdfs.sh
```

# Run the viser simulation for Indy 7
```bash
cd ~/workspaces/movensys_ws/src/pyroki
pyr example/01_basic_ik.py
```