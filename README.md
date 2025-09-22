# robot_hardware

ros2_control SystemInterface / Hardware Bridge - Host-Seite (SBC). Diese Komponente verbindet ROS 2 controller_manager mit der Digital-Board Firmware (Pico).

## Zweck
- Implementiert hardware_interface::SystemInterface (C++) oder Bridge Node (Python) für:
  - read(): Encoder -> joint state
  - write(): wheel commands -> send to Pico

## Wichtige Dateien
- src/ - Hardware Interface (C++) oder bridge node
- include/ - Header (bei C++)
- config/ros2_control_params.yaml - Beispiel params
- multi_drive_hardware_plugins.xml - pluginlib Export

## Konfiguration (Beispiel)
- In ros2_control params:
  - serial_port: /dev/ttyACM0
  - baudrate: 115200
  - drive_type: mecanum|diff
  - joint names: list mit wheel_*_joint

## Entwicklung & Tests
- Entwickle zuerst mit Fake-Hardware: read() liefert deterministische Encoderwerte.
- Serial implementieren mit boost::asio oder serialib.
- Unit tests: Simulierter serial input -> state updates.
