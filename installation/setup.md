# Install ROS2
## 1. For Ubuntu 22.04, install ROS2 Humble
- Follow https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debs.html

## 2. For Ubuntu 24.04, install ROS2 Jazzy
- Follow https://docs.ros.org/en/jazzy/Installation/Ubuntu-Install-Debs.html

# Set .bashrc configuration
- Run below commands on the terminal
```bash
cat >> ~/.bashrc << 'EOF'

export ROS_DOMAIN_ID=34                         #use any number
export ROS_DISTRO=jazzy                         #support {jazzy, humble}
source /opt/ros/$ROS_DISTRO/setup.bash
source ~/workspaces/movensys_ws/install/setup.bash
alias pyr='env -u PYTHONPATH JAX_PLATFORMS=cpu ~/workspaces/movensys_ws/src/pyroki/.venv/bin/python'
EOF
```

- Open the new terminal and check the ros2 is installed or not.
```bash
ros2 topic list
```


# Install Pyroki in user workspace
```bash
source ~/.bashrc
mkdir -p ~/workspaces/movensys_ws/src
cd ~/workspaces/movensys_ws/src
git clone https://github.com/LayNoah/pyroki.git
```

# Create the Python venv for Pyroki
```bash
sudo apt-get install python3-venv git ros-$ROS_DISTRO-xacro
cd ~/workspaces/movensys_ws/src/pyroki
python3 -m venv .venv
env -u PYTHONPATH .venv/bin/pip install --upgrade pip
env -u PYTHONPATH .venv/bin/pip install -e .
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
ros2 run xacro xacro indy7_standalone.xacro -o ../urdf_files/indy7_gripper.urdf
```

# Run the viser simulation for Indy 7
```bash
cd ~/workspaces/movensys_ws/src/pyroki
pyr examples/01_basic_ik.py
```