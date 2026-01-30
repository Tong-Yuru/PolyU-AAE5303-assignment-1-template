# AAE5303 Environment Setup Report — Template for Students

> **Important:** Follow this structure exactly in your submission README.  
> Your goal is to demonstrate **evidence, process, problem-solving, and reflection** — not only screenshots.

---

## 1. System Information

**Laptop model:**  LAPTOP-50SB5BCQ

**CPU / RAM:**  11th Gen Intel(R) Core(TM) i5-1135G7 @ 2.40GHz，16GB RAM

**Host OS:**  Windows 10

**Linux/ROS environment type:**  
- [ ] Dual-boot Ubuntu
- [√] WSL2 Ubuntu
- [ ] Ubuntu in VM (UTM/VirtualBox/VMware/Parallels)
- [ ] Docker container
- [ ] Lab PC
- [ ] Remote Linux server

---

## 2. Python Environment Check

### 2.1 Steps Taken

Describe briefly how you created/activated your Python environment:

**Tool used:**  venv

**Key commands you ran:**
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

**Any deviations from the default instructions:**  None

### 2.2 Test Results

Run these commands and paste the actual terminal output (not just screenshots):

```bash
python scripts/run_smoke_tests.py
```

**Output:**
```
[========================================
AAE5303 One-command Environment Check
Tip: read README.md for interpretation and fixes.
========================================


========== Step 1: Python + ROS environment checks ==========
Running: /home/aae/PolyU-AAE5303-env-smork-test/.venv/bin/python -u /home/aae/PolyU-AAE5303-env-smork-test/scripts/test_python_env.py
========================================
AAE5303 Environment Check (Python + ROS)
Goal: help you verify your environment and understand what each check means.
========================================

Step 1: Environment snapshot
  Why: We capture platform/Python/ROS variables to diagnose common setup mistakes (especially mixed ROS env).
Step 2: Python version
  Why: The course assumes Python 3.10+; older versions often break package wheels.
Step 3: Python imports (required/optional)
  Why: Imports verify packages are installed and compatible with your Python version.
Step 4: NumPy sanity checks
  Why: We run a small linear algebra operation so success means more than just `import numpy`.
Step 5: SciPy sanity checks
  Why: We run a small FFT to confirm SciPy is functional (not just installed).
Step 6: Matplotlib backend check
  Why: We generate a tiny plot image (headless) to confirm plotting works on your system.
Step 7: OpenCV PNG decoding (subprocess)
  Why: PNG decoding uses native code; we isolate it so corruption/codec issues cannot crash the whole report.
Step 8: Open3D basic geometry + I/O (subprocess)
  Why: Open3D is a native extension; ABI mismatches can segfault. Subprocess isolation turns crashes into readable failures.
Step 9: ROS toolchain checks
  Why: The course requires ROS tooling. This check passes if ROS 2 OR ROS 1 is available (either one is acceptable).
  Action: building ROS 2 workspace package `env_check_pkg` (this may take 1-3 minutes on first run)...
  Action: running ROS 2 talker/listener for a few seconds to verify messages flow...
Step 10: Basic CLI availability
  Why: We confirm core commands exist on PATH so students can run the same commands as in the labs.

=== Summary ===
✅ Environment: {
  "platform": "Linux-6.6.87.2-microsoft-standard-WSL2-x86_64-with-glibc2.35",
  "python": "3.10.12",
  "executable": "/home/aae/PolyU-AAE5303-env-smork-test/.venv/bin/python",
  "cwd": "/home/aae/PolyU-AAE5303-env-smork-test",
  "ros": {
    "ROS_VERSION": "2",
    "ROS_DISTRO": "humble",
    "ROS_ROOT": null,
    "ROS_PACKAGE_PATH": null,
    "AMENT_PREFIX_PATH": "/opt/ros/humble",
    "CMAKE_PREFIX_PATH": null
  }
}
✅ Python version OK: 3.10.12
✅ Module 'numpy' found (v2.2.6).
✅ Module 'scipy' found (v1.15.3).
✅ Module 'matplotlib' found (v3.10.8).
✅ Module 'cv2' found (v4.13.0).
✅ Module 'rclpy' found (vunknown).
✅ numpy matrix multiply OK.
✅ numpy version 2.2.6 detected.
✅ scipy FFT OK.
✅ scipy version 1.15.3 detected.
✅ matplotlib backend OK (Agg), version 3.10.8.
✅ OpenCV OK (v4.13.0), decoded sample image 128x128.
✅ Open3D OK (v0.19.0), NumPy 2.2.6.
✅ Open3D loaded sample PCD with 8 pts and completed round-trip I/O.
✅ ROS 2 CLI OK: /opt/ros/humble/bin/ros2
✅ ROS 1 tools not found (acceptable if ROS 2 is installed).
✅ colcon found: /usr/bin/colcon
✅ ROS 2 workspace build OK (env_check_pkg).
✅ ROS 2 runtime OK: talker and listener exchanged messages.
✅ Binary 'python3' found at /home/aae/PolyU-AAE5303-env-smork-test/.venv/bin/python3

All checks passed. You are ready for AAE5303 🚀
✅ Python + ROS environment checks: PASS (4.1s)]
```

```bash
python scripts/test_open3d_pointcloud.py
```

**Output:**
```
[========== Step 2: Open3D point cloud pipeline ==========
Running: /home/aae/PolyU-AAE5303-env-smork-test/.venv/bin/python -u /home/aae/PolyU-AAE5303-env-smork-test/scripts/test_open3d_pointcloud.py
ℹ️ Loading /home/aae/PolyU-AAE5303-env-smork-test/data/sample_pointcloud.pcd ...
✅ Loaded 8 points.
   • Centroid: [0.025 0.025 0.025]
   • Axis-aligned bounds: min=[0. 0. 0.], max=[0.05 0.05 0.05]
✅ Filtered point cloud kept 7 points.
✅ Wrote filtered copy with 7 points to /home/aae/PolyU-AAE5303-env-smork-test/data/sample_pointcloud_copy.pcd
   • AABB extents: [0.05 0.05 0.05]
   • OBB  extents: [0.08164966 0.07071068 0.05773503], max dim 0.0816 m
🎉 Open3D point cloud pipeline looks good.
✅ Open3D point cloud pipeline: PASS (1.8s)

ℹ️ Cleaned up 1 generated file(s) in data/.

========================================
OVERALL RESULT: PASS
========================================]
```

**Screenshot:**  
_[<img width="2999" height="1937" alt="Python Test Passing" src="https://github.com/user-attachments/assets/10aa9d37-9019-4f60-83d0-a0a0edb46ae4" />]_

---

## 3. ROS 2 Workspace Check

### 3.1 Build the workspace

Paste the build output summary (final lines only):

```bash
source /opt/ros/humble/setup.bash
colcon build
```

**Expected output:**
```
Summary: 1 package finished [x.xx s]
```

**Your actual output:**
```
Starting >>> env_check_pkg
Finished <<< env_check_pkg [0.21s]

Summary: 1 package finished [0.69s]
```

### 3.2 Run talker and listener

Show both source commands:

```bash
source /opt/ros/humble/setup.bash
source install/setup.bash
```

**Then run talker:**
```bash
ros2 run env_check_pkg talker.py
```

**Output (3–4 lines):**
```
[INFO] [1769764647.765488242] [env_check_pkg_talker]: AAE5303 talker ready (publishing at 2 Hz).
[INFO] [1769764648.315745312] [env_check_pkg_talker]: Publishing: 'AAE5303 hello #0'
[INFO] [1769764648.866021522] [env_check_pkg_talker]: Publishing: 'AAE5303 hello #1'
[INFO] [1769764648.919595236] [env_check_pkg_talker]: Publishing: 'AAE5303 hello #2'
[INFO] [1769764649.469803686] [env_check_pkg_talker]: Publishing: 'AAE5303 hello #3'
[INFO] [1769764650.019786636] [env_check_pkg_talker]: Publishing: 'AAE5303 hello #4'
```

**Run listener:**
```bash
ros2 run env_check_pkg listener.py
```

**Output (3–4 lines):**
```
[INFO] [1769765442.460240780] [env_check_pkg_listener]: AAE5303 listener awaiting messages.
[INFO] [1769765442.706895210] [env_check_pkg_listener]: I heard: 'AAE5303 hello #144'
[INFO] [1769765443.256975510] [env_check_pkg_listener]: I heard: 'AAE5303 hello #145'
[INFO] [1769765443.806943500] [env_check_pkg_listener]: I heard: 'AAE5303 hello #146'
[INFO] [1769765444.356485020] [env_check_pkg_listener]: I heard: 'AAE5303 hello #147'
[INFO] [1769765444.906832620] [env_check_pkg_listener]: I heard: 'AAE5303 hello #148'
```

**Alternative (using launch file):**
```bash
ros2 launch env_check_pkg env_check.launch.py
```

**Screenshot:**  
<img width="1957" height="1289" alt="talker_listener" src="https://github.com/user-attachments/assets/8160a2d1-5240-40a0-be1c-bd084d3df1a5" />



---

## 4. Problems Encountered and How I Solved Them

> **Note:** Write 2–3 issues, even if small. This section is crucial — it demonstrates understanding and problem-solving.

### Issue 1:Failed to create Python virtual environment (error: "ensurepip is not available")

**Cause / diagnosis:**  
My Ubuntu 22.04 system lacked the python3.10-venv package, which is required to create Python virtual environments using python3 -m venv.

**Fix:**  
Install the missing package, then recreate the virtual environment:

```bash
# Install the required venv package
sudo apt install python3.10-venv -y
# Delete the incomplete virtual environment
rm -rf .venv
# Recreate the virtual environment
python3 -m venv .venv
```

**Reference:**  
System error message prompt + AI assistant.

---

### Issue 2: ROS 2 workspace build failed (error: "ROS 2 workspace build failed (exit 1)")

**Cause / diagnosis:**  
Residual files (build, install, log) from a previous failed build caused conflicts, and I was missing ROS 2 C++ dependencies needed for the env_check_pkg package.

**Fix:**  
Delete residual build files and install required ROS 2 dependencies:

```bash
# Navigate to the ROS 2 workspace
cd ~/PolyU-AAE5303-env-smork-test/ros2_ws
# Delete residual build files
rm -rf build install log
# Install ROS 2 C++ dependencies
sudo apt install -y ros-humble-rclcpp ros-humble-std-msgs
# Rebuild the package
colcon build --packages-select env_check_pkg
```

**Reference:**  
System error message prompt + AI assistant.

---

### Issue 3 (Optional):Colcon build failed (error: "ModuleNotFoundError: No module named 'catkin_pkg'")

**Cause / diagnosis:**  
The catkin_pkg module (required for parsing ROS package files) was missing, and I was running the build in a Python virtual environment (which couldn’t access the system-level catkin_pkg).

**Fix:**  
Install catkin_pkg (system + virtual environment) and build outside the virtual environment:

```bash
# Install system-level catkin_pkg
sudo apt install -y python3-catkin-pkg
# Install catkin_pkg in the virtual environment
pip install catkin-pkg
# Exit the virtual environment
deactivate
# Reload ROS 2 environment and rebuild
source /opt/ros/humble/setup.bash
cd ~/PolyU-AAE5303-env-smork-test/ros2_ws
rm -rf build install log
colcon build --packages-select env_check_pkg
```

**Reference:**  
AI assistant + ROS 2 official documentation.

---

## 5. Use of Generative AI (Required)

Choose one of the issues above and document how you used AI to solve it.

> **Goal:** Show critical use of AI, not blind copying.

### 5.1 Exact prompt you asked

**Your prompt:**
```
执行“colcon build --packages-select env_check_pkg”后系统显示：Starting >>> env_check_pkg --- stderr: env_check_pkg Traceback (most recent call last): File "/opt/ros/humble/share/ament_cmake_core/cmake/core/package_xml_2_cmake.py", line 22, in <module> from catkin_pkg.package import parse_package_string ModuleNotFoundError: No module named 'catkin_pkg' CMake Error at /opt/ros/humble/share/ament_cmake_core/cmake/core/ament_package_xml.cmake:95 (message): execute_process(/home/aae/PolyU-AAE5303-env-smork-test/.venv/bin/python3 /opt/ros/humble/share/ament_cmake_core/cmake/core/package_xml_2_cmake.py /home/aae/PolyU-AAE5303-env-smork-test/ros2_ws/src/env_check_pkg/package.xml /home/aae/PolyU-AAE5303-env-smork-test/ros2_ws/build/env_check_pkg/ament_cmake_core/package.cmake) returned error code 1 Call Stack (most recent call first): /opt/ros/humble/share/ament_cmake_core/cmake/core/ament_package_xml.cmake:49 (_ament_package_xml) /opt/ros/humble/share/ament_lint_auto/cmake/ament_lint_auto_find_test_dependencies.cmake:31 (ament_package_xml) CMakeLists.txt:28 (ament_lint_auto_find_test_dependencies) --- Failed <<< env_check_pkg [4.53s, exited with code 1] Summary: 0 packages finished [4.99s] 1 package failed: env_check_pkg 1 package had stderr output: env_check_pkg,这是怎么回事啊？我应该怎么改？
```

### 5.2 Key helpful part of the AI's answer

**AI's response (relevant part only):**
```
The error happens because: 1) The 'catkin_pkg' module (required for ROS package parsing) is missing. 2) You're in a Python virtual environment, which can't access the system-level 'catkin_pkg'.

Fix steps:
1. Install 'catkin_pkg' both system-wide and in the virtual environment:
   sudo apt install -y python3-catkin-pkg
   pip install catkin-pkg
2. Exit the virtual environment (run 'deactivate') before building ROS 2 workspace.
3. Reload ROS 2 environment and rebuild:
   source /opt/ros/humble/setup.bash
   cd ~/PolyU-AAE5303-env-smork-test/ros2_ws
   rm -rf build install log
   colcon build --packages-select env_check_pkg
```

### 5.3 What you changed or ignored and why

Explain briefly:
- Did the AI recommend something unsafe?
- Did you modify its solution?
- Did you double-check with official docs?

**Your explanation:**  
The AI didn’t recommend anything unsafe.
I didn’t modify its solution (it matched my environment’s needs).
I double-checked the "ROS 2 Humble Installation Guide" to confirm that 'catkin_pkg' is a required dependency for package building, which verified the AI’s advice.

### 5.4 Final solution you applied

Show the exact command or file edit that fixed the problem:

```bash
# Install system-level catkin_pkg
sudo apt install -y python3-catkin-pkg
# Install catkin_pkg in virtual environment
pip install catkin-pkg
# Exit virtual environment
deactivate
# Reload ROS 2 environment and rebuild
source /opt/ros/humble/setup.bash
cd ~/PolyU-AAE5303-env-smork-test/ros2_ws
rm -rf build install log
colcon build --packages-select env_check_pkg
```

**Why this worked:**  
Installing 'catkin_pkg' resolved the missing module error. Exiting the virtual environment let ROS 2 access system-level dependencies, and deleting residual build files eliminated conflicts—allowing the workspace to build successfully.

---

## 6. Reflection (3–5 sentences)

Short but thoughtful:

- What did you learn about configuring robotics environments?
- What surprised you?
- What would you do differently next time (backup, partitioning, reading error logs, asking better AI questions)?
- How confident do you feel about debugging ROS/Python issues now?

**Your reflection:**

Configuring robotics environments taught me that small details (like virtual environment vs. system Python) can break complex tools like ROS 2, so isolating environment contexts is critical. I was surprised by how interconnected dependencies are—missing one small package (like 'python3.10-venv') could halt the entire setup. Next time, I’ll read error logs more carefully first (instead of panicking) and include environment context (e.g., "I’m in a virtual environment") in AI prompts to get more targeted advice. I now feel moderately confident debugging basic ROS/Python issues, as I’ve learned to trace errors to missing dependencies or environment conflicts.

---

## 7. Declaration

✅ **I confirm that I performed this setup myself and all screenshots/logs reflect my own environment.**

**Name:**  
Tong Yuru

**Student ID:**  
25106011G

**Date:**  
2026/1/30

---

## Submission Checklist

Before submitting, ensure you have:

- [√] Filled in all system information
- [√] Included actual terminal outputs (not just screenshots)
- [√] Provided at least 2 screenshots (Python tests + ROS talker/listener)
- [√] Documented 2–3 real problems with solutions
- [√] Completed the AI usage section with exact prompts
- [√] Written a thoughtful reflection (3–5 sentences)
- [√] Signed the declaration

---

**End of Report**
