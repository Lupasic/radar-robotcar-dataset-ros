# ROS2 Bag Recording Implementation - Test Guide

## What has been implemented:

### 1. **Save Button Enhancement**
- The save button now starts ROS2 bag recording when clicked
- It collects topics from all enabled sensors automatically
- Shows recording status in the UI

### 2. **Topic Collection**
The following topics are recorded based on sensor selections:

**Stereo Camera:**
- `/robotcar/stereo/left`
- `/robotcar/stereo/centre` 
- `/robotcar/stereo/right`

**Mono Cameras:**
- `/robotcar/mono/left`
- `/robotcar/mono/right`
- `/robotcar/mono/rear`

**Radar:**
- `/robotcar/radar/polar`
- `/robotcar/radar/cart`

**3D LiDARs:**
- `/robotcar/lidar/left`
- `/robotcar/lidar/right`

**2D LiDARs:**
- `/robotcar/lidar/front`
- `/robotcar/lidar/rear`

**LiDAR Old (3D front):**
- `/robotcar/lidar/front3d`

**GPS/INS:**
- `/robotcar/ins/gps`
- `/robotcar/ins/odom`

**Always Recorded:**
- `/tf`
- `/tf_static`

### 3. **Workflow**
1. **Setup**: Select dataset path and SDK path
2. **Sensor Selection**: Check the sensors you want to record
3. **Save Setup**: Click "Save" button, choose output location
4. **Recording Starts**: ROS2 bag record starts automatically
5. **Data Flow**: Click "Play" to start publishing sensor data
6. **Stop Recording**: Click "Abort" to stop playback and recording

### 4. **UI Feedback**
- Save button changes to "Recording..." when active
- Status text shows which topics are being recorded
- Error messages for any recording issues
- Success confirmation when recording completes

### 5. **Process Management**
- Uses QProcess to manage ros2 bag record command
- Proper cleanup on application close
- Graceful termination with SIGTERM, then SIGKILL if needed

## Testing Steps:

1. Build and run the application
2. Select some sensors (e.g., stereo camera, radar)
3. Click "Save" and choose output directory
4. Check that recording starts (button text changes)
5. Click "Play" to start data flow
6. Click "Abort" to stop everything
7. Verify the bag file is created in the chosen location

## Command that gets executed:
```bash
ros2 bag record -o <output_path> <selected_topics> /tf /tf_static
```

Example:
```bash
ros2 bag record -o /path/to/output /robotcar/stereo/left /robotcar/stereo/centre /robotcar/stereo/right /robotcar/radar/polar /robotcar/radar/cart /tf /tf_static
```
