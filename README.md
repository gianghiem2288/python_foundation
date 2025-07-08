# python_foundation
Python basic theory
# Python Basics for IoT Development

## Table of Contents
1. [Variables](#1-variables)
2. [Data Types](#2-data-types)
3. [Functions and Modules](#3-functions-and-modules)
4. [Classes and Objects](#4-classes-and-objects)
5. [External Imports](#5-external-imports)
6. [IoT Project Example](#6-iot-project-example)

## 1. Variables

Trong Python, biến (variables) là nơi lưu trữ các giá trị dữ liệu. Python là một ngôn ngữ kiểu động (dynamically typed), nghĩa là không cần khai báo kiểu dữ liệu khi tạo biến.

### Cách khai báo biến

```python
# Khai báo biến đơn giản
temperature = 25
device_name = "Temperature Sensor"
is_active = True

# Khai báo nhiều biến cùng lúc
x, y, z = 10, "Hello", False

# Hằng số (thực chất Python không có hằng số, chỉ là quy ước đặt tên)
MAX_TEMPERATURE = 100
MIN_TEMPERATURE = 0
```

### Quy tắc đặt tên biến
- Tên biến phải bắt đầu bằng chữ cái hoặc dấu gạch dưới (_)
- Không được bắt đầu bằng số
- Chỉ được chứa các ký tự chữ cái, số, và dấu gạch dưới (a-z, A-Z, 0-9, _)
- Phân biệt chữ hoa, chữ thường (case-sensitive)

### Phạm vi biến (Variable Scope)

```python
# Biến toàn cục (Global variable)
global_var = "Tôi là biến toàn cục"

def my_function():
    # Biến cục bộ (Local variable)
    local_var = "Tôi là biến cục bộ"
    print(global_var)  # Có thể truy cập biến toàn cục
    print(local_var)   # Có thể truy cập biến cục bộ

my_function()
print(global_var)      # Có thể truy cập biến toàn cục
# print(local_var)     # Lỗi: local_var không tồn tại ở phạm vi này
```

### Sử dụng từ khóa global

```python
counter = 0

def increase_counter():
    global counter  # Khai báo sử dụng biến toàn cục
    counter += 1
    print(f"Counter: {counter}")

increase_counter()  # Counter: 1
increase_counter()  # Counter: 2
```

## 2. Data Types

Python có nhiều kiểu dữ liệu từ cơ bản đến phức tạp. Dưới đây là các kiểu dữ liệu chính:

### Kiểu dữ liệu cơ bản

#### Numbers (Số)

```python
# Integer (Số nguyên)
temperature = 25
sensor_count = -3

# Float (Số thực)
humidity = 67.8
pressure = 1013.25

# Complex (Số phức)
complex_number = 3 + 4j
```

#### Boolean (Logic)

```python
is_connected = True
is_error = False

# Boolean từ biểu thức so sánh
is_high_temp = temperature > 30  # False nếu temperature = 25
```

#### String (Chuỗi)

```python
device_id = "TempSensor01"
device_location = 'Room 203'

# Chuỗi nhiều dòng
description = """This is a temperature sensor
that measures ambient temperature
in Celsius."""

# Định dạng chuỗi
model = "DHT11"
message = f"Sensor {device_id} model {model} đang hoạt động"

# Các phương thức chuỗi hữu ích
print(device_id.upper())         # TEMPSENSOR01
print(device_location.replace("Room", "Office"))  # Office 203
print(len(description))          # Độ dài chuỗi
print("temp" in device_id)       # True - kiểm tra chuỗi con
```

#### None

```python
sensor_error = None  # Biểu thị giá trị không tồn tại hoặc chưa được gán
```

### Kiểu dữ liệu cấu trúc (Collections)

#### List (Danh sách)

```python
# Danh sách các giá trị cảm biến
temperature_readings = [21.5, 22.1, 22.4, 22.8, 23.0]

# Danh sách có thể chứa nhiều kiểu dữ liệu
mixed_list = [1, "sensor", True, 23.5]

# Truy cập phần tử
print(temperature_readings[0])    # 21.5 (phần tử đầu tiên)
print(temperature_readings[-1])   # 23.0 (phần tử cuối cùng)
print(temperature_readings[1:3])  # [22.1, 22.4] (cắt danh sách)

# Các phương thức của list
temperature_readings.append(23.2)  # Thêm phần tử
temperature_readings.sort()        # Sắp xếp
temperature_readings.reverse()     # Đảo ngược
print(len(temperature_readings))   # Độ dài danh sách
```

#### Tuple (Bộ giá trị)

```python
# Tuple - không thể thay đổi sau khi tạo
sensor_location = (40.7128, -74.0060)  # Vĩ độ, kinh độ
rgb_color = (255, 0, 128)

# Truy cập phần tử tuple giống như list
latitude = sensor_location[0]   # 40.7128
longitude = sensor_location[1]  # -74.0060

# Giải nén tuple
lat, lng = sensor_location
r, g, b = rgb_color
```

#### Dictionary (Từ điển)

```python
# Dictionary lưu trữ cặp key-value
sensor = {
    "id": "TempSensor01",
    "type": "Temperature",
    "value": 25.5,
    "unit": "Celsius",
    "is_active": True
}

# Truy cập giá trị
print(sensor["id"])      # TempSensor01
print(sensor.get("type"))  # Temperature

# Thêm hoặc cập nhật phần tử
sensor["battery"] = 85  # Thêm mới
sensor["value"] = 26.1  # Cập nhật

# Các phương thức hữu ích
print(sensor.keys())    # Lấy tất cả các key
print(sensor.values())  # Lấy tất cả các value
print(sensor.items())   # Lấy tất cả các cặp key-value
```

#### Set (Tập hợp)

```python
# Set - tập hợp các phần tử duy nhất không thứ tự
sensor_types = {"Temperature", "Humidity", "Pressure", "Temperature"}
print(sensor_types)  # {'Humidity', 'Pressure', 'Temperature'} - trùng lặp bị loại bỏ

# Các phép toán tập hợp
sensors_room_1 = {"Temp1", "Humid1", "Press1"}
sensors_room_2 = {"Temp2", "Humid2", "Temp1"}

# Hợp (Union)
all_sensors = sensors_room_1 | sensors_room_2

# Giao (Intersection)
common_sensors = sensors_room_1 & sensors_room_2  # {'Temp1'}

# Hiệu (Difference)
only_in_room_1 = sensors_room_1 - sensors_room_2  # {'Humid1', 'Press1'}
```

### Kiểu dữ liệu nâng cao

#### Bytes và ByteArray

```python
# Bytes - chuỗi byte không thể thay đổi
message_bytes = b'Hello IoT'
hex_bytes = bytes.fromhex('68 65 6c 6c 6f')  # hello

# ByteArray - chuỗi byte có thể thay đổi
mutable_bytes = bytearray(b'Hello')
mutable_bytes[0] = 74  # Thay đổi 'H' thành 'J'
print(mutable_bytes)  # bytearray(b'Jello')

# Hữu ích khi làm việc với giao thức truyền thông IoT
```

## 3. Functions and Modules

### Functions (Hàm)

Hàm là khối mã có thể tái sử dụng thực hiện một tác vụ cụ thể.

#### Định nghĩa và gọi hàm

```python
# Hàm đơn giản
def greet_device(device_name):
    return f"Hello {device_name}!"

# Gọi hàm
message = greet_device("Temperature Sensor")
print(message)  # Hello Temperature Sensor!
```

#### Tham số của hàm

```python
# Tham số mặc định
def connect_device(device_id, timeout=30, retry=3):
    print(f"Connecting to {device_id} with timeout={timeout}s, retry={retry}")
    # Mã kết nối thiết bị

# Gọi hàm với các tham số khác nhau
connect_device("dev001")  # Sử dụng giá trị mặc định cho timeout và retry
connect_device("dev002", 60)  # Tùy chỉnh timeout
connect_device("dev003", retry=5)  # Chỉ định tham số theo tên
```

#### Args và Kwargs

```python
# *args - nhận nhiều tham số dạng tuple
def calculate_average(*values):
    return sum(values) / len(values)

avg = calculate_average(21.5, 22.1, 22.8, 23.0)
print(f"Average: {avg}")  # Average: 22.35

# **kwargs - nhận nhiều tham số dạng dictionary
def configure_sensor(**settings):
    print("Configuring sensor with settings:")
    for key, value in settings.items():
        print(f"  {key}: {value}")

configure_sensor(interval=5, precision=0.01, alert_threshold=30)
```

#### Lambda Functions (Hàm ẩn danh)

```python
# Hàm lambda - hàm ngắn, không tên
celsius_to_fahrenheit = lambda c: (c * 9/5) + 32

# Sử dụng lambda
print(celsius_to_fahrenheit(25))  # 77.0

# Hữu ích với các hàm như map, filter
temperatures = [20, 22, 25, 28, 30]
fahrenheit_temps = list(map(celsius_to_fahrenheit, temperatures))
high_temps = list(filter(lambda t: t > 25, temperatures))
```

### Modules (Mô-đun)

Module là tệp Python chứa các định nghĩa và câu lệnh có thể sử dụng lại trong chương trình khác.

#### Tạo và sử dụng module

Giả sử chúng ta có một file `sensor_utils.py`:

```python
# File: sensor_utils.py
def celsius_to_fahrenheit(celsius):
    return (celsius * 9/5) + 32

def fahrenheit_to_celsius(fahrenheit):
    return (fahrenheit - 32) * 5/9

def kelvin_to_celsius(kelvin):
    return kelvin - 273.15

# Hằng số
ABSOLUTE_ZERO_C = -273.15
```

Sử dụng module:

```python
# Nhập toàn bộ module
import sensor_utils

temp_f = sensor_utils.celsius_to_fahrenheit(25)
print(f"25°C = {temp_f}°F")

# Nhập các hàm cụ thể
from sensor_utils import fahrenheit_to_celsius, ABSOLUTE_ZERO_C

temp_c = fahrenheit_to_celsius(77)
print(f"77°F = {temp_c}°C")
print(f"Absolute zero: {ABSOLUTE_ZERO_C}°C")

# Nhập tất cả (không khuyến khích)
from sensor_utils import *

kelvin = 300
celsius = kelvin_to_celsius(kelvin)
```

#### Tổ chức các module thành package

Packages là cách tổ chức các module vào một cấu trúc thư mục.

Cấu trúc thư mục ví dụ:
```
iot_project/
│
├── __init__.py         # Biến thư mục thành package
├── sensors/
│   ├── __init__.py
│   ├── temperature.py
│   └── humidity.py
└── utils/
    ├── __init__.py
    ├── conversion.py
    └── network.py
```

Sử dụng package:

```python
# Nhập module từ package
from iot_project.sensors import temperature
from iot_project.utils.conversion import celsius_to_fahrenheit

# Sử dụng các hàm từ module
temp_sensor = temperature.TemperatureSensor("dev001")
temp_f = celsius_to_fahrenheit(temp_sensor.read())
```

## 4. Classes and Objects

Lập trình hướng đối tượng (OOP) trong Python sử dụng các class (lớp) để tạo ra objects (đối tượng).

### Class và Objects

```python
# Định nghĩa class
class Sensor:
    # Thuộc tính lớp (class attribute)
    sensor_count = 0
    
    # Phương thức khởi tạo (constructor)
    def __init__(self, sensor_id, sensor_type, unit):
        # Thuộc tính đối tượng (instance attributes)
        self.sensor_id = sensor_id
        self.sensor_type = sensor_type
        self.unit = unit
        self.is_active = False
        self.value = None
        
        # Tăng biến đếm khi tạo đối tượng mới
        Sensor.sensor_count += 1
    
    # Phương thức đối tượng (instance method)
    def activate(self):
        self.is_active = True
        print(f"Sensor {self.sensor_id} activated")
    
    def deactivate(self):
        self.is_active = False
        print(f"Sensor {self.sensor_id} deactivated")
    
    def read_value(self):
        if not self.is_active:
            return "Error: Sensor is not active"
        # Giả lập đọc giá trị từ cảm biến
        import random
        self.value = random.uniform(20, 30)
        return f"{self.value} {self.unit}"
    
    # Phương thức biểu diễn chuỗi
    def __str__(self):
        status = "active" if self.is_active else "inactive"
        return f"Sensor(id={self.sensor_id}, type={self.sensor_type}, status={status})"

# Tạo đối tượng từ class
temp_sensor = Sensor("temp001", "Temperature", "°C")
humidity_sensor = Sensor("hum001", "Humidity", "%")

# Sử dụng các phương thức và thuộc tính
temp_sensor.activate()
print(temp_sensor.read_value())  # Ví dụ: 24.5 °C

print(f"Total sensors: {Sensor.sensor_count}")  # Total sensors: 2
print(temp_sensor)  # Sensor(id=temp001, type=Temperature, status=active)
```

### Kế thừa (Inheritance)

```python
# Class cha
class Sensor:
    def __init__(self, sensor_id):
        self.sensor_id = sensor_id
        self.is_active = False
        
    def activate(self):
        self.is_active = True
        print(f"Sensor {self.sensor_id} activated")
        
    def read_value(self):
        if not self.is_active:
            return "Error: Sensor not active"
        return "No data: read_value() method should be implemented by subclass"

# Class con kế thừa từ Sensor
class TemperatureSensor(Sensor):
    def __init__(self, sensor_id, min_temp=-40, max_temp=80):
        # Gọi constructor của class cha
        super().__init__(sensor_id)
        self.min_temp = min_temp
        self.max_temp = max_temp
        self.unit = "°C"
    
    # Override phương thức của class cha
    def read_value(self):
        if not self.is_active:
            return "Error: Sensor not active"
        import random
        temp = random.uniform(15, 35)
        return f"{temp:.1f} {self.unit}"

# Class con khác
class HumiditySensor(Sensor):
    def __init__(self, sensor_id):
        super().__init__(sensor_id)
        self.unit = "%"
    
    def read_value(self):
        if not self.is_active:
            return "Error: Sensor not active"
        import random
        humidity = random.uniform(30, 90)
        return f"{humidity:.1f} {self.unit}"

# Sử dụng các class con
temp_sensor = TemperatureSensor("temp002")
temp_sensor.activate()
print(f"Temperature: {temp_sensor.read_value()}")

hum_sensor = HumiditySensor("hum002")
hum_sensor.activate()
print(f"Humidity: {hum_sensor.read_value()}")
```

### Thuộc tính đặc biệt

```python
class IoTDevice:
    def __init__(self, device_id, device_name):
        self._device_id = device_id  # Thuộc tính "private" (quy ước)
        self.device_name = device_name
        self.__secret_key = "12345"  # Thuộc tính "thực sự private" (name mangling)
    
    # Getter và Setter sử dụng @property
    @property
    def device_id(self):
        return self._device_id
    
    @device_id.setter
    def device_id(self, value):
        if not value.strip():
            raise ValueError("Device ID cannot be empty")
        self._device_id = value
    
    # Phương thức tĩnh (static method) - không cần truy cập vào đối tượng
    @staticmethod
    def is_valid_id(device_id):
        return bool(device_id and device_id.startswith("DEV"))
    
    # Phương thức lớp (class method) - nhận class làm tham số đầu tiên
    @classmethod
    def create_from_serial(cls, serial_number):
        device_id = f"DEV-{serial_number}"
        return cls(device_id, f"Device {serial_number}")

# Sử dụng thuộc tính đặc biệt
device = IoTDevice("DEV001", "Temperature Controller")
print(device.device_id)  # DEV001 (sử dụng getter)

device.device_id = "DEV002"  # Sử dụng setter
# device.device_id = ""  # Lỗi: Device ID cannot be empty

# Sử dụng phương thức tĩnh
print(IoTDevice.is_valid_id("DEV003"))  # True
print(IoTDevice.is_valid_id("123"))     # False

# Sử dụng phương thức lớp
new_device = IoTDevice.create_from_serial("A12345")
print(new_device.device_id, new_device.device_name)  # DEV-A12345 Device A12345
```

## 5. External Imports

Python có một hệ sinh thái thư viện phong phú. Đây là cách sử dụng các thư viện ngoài:

### Cài đặt thư viện ngoài

Sử dụng pip, công cụ quản lý gói của Python:

```bash
# Cài đặt một gói
pip install requests

# Cài đặt phiên bản cụ thể
pip install requests==2.26.0

# Cài đặt nhiều gói
pip install requests pandas matplotlib

# Cài đặt từ requirements file
pip install -r requirements.txt
```

### Sử dụng thư viện ngoài

```python
# Thư viện requests để thực hiện HTTP requests
import requests

# Gửi HTTP GET request
response = requests.get('https://api.example.com/data')
if response.status_code == 200:
    data = response.json()
    print(f"Received data: {data}")
else:
    print(f"Error: {response.status_code}")

# Gửi HTTP POST request với dữ liệu
sensor_data = {
    "device_id": "temp001",
    "temperature": 25.4,
    "humidity": 67.8,
    "timestamp": "2025-07-08T15:45:30Z"
}

headers = {'Content-Type': 'application/json'}
response = requests.post('https://api.example.com/submit', 
                        json=sensor_data, 
                        headers=headers)

print(f"Status code: {response.status_code}")
print(f"Response: {response.text}")
```

### Thư viện phổ biến cho IoT

```python
# GPIO trên Raspberry Pi
import RPi.GPIO as GPIO

# Thiết lập mode cho GPIO
GPIO.setmode(GPIO.BCM)
# Cấu hình chân GPIO 18 là OUTPUT
GPIO.setup(18, GPIO.OUT)
# Bật LED
GPIO.output(18, GPIO.HIGH)
# Tắt LED
GPIO.output(18, GPIO.LOW)
# Dọn dẹp
GPIO.cleanup()

# MQTT cho IoT messaging
import paho.mqtt.client as mqtt

# Callback khi kết nối thành công
def on_connect(client, userdata, flags, rc):
    print(f"Connected with result code {rc}")
    # Đăng ký nhận tin nhắn từ topic
    client.subscribe("home/sensors/#")

# Callback khi nhận được tin nhắn
def on_message(client, userdata, msg):
    print(f"Message from {msg.topic}: {msg.payload.decode()}")

# Tạo client
client = mqtt.Client()
client.on_connect = on_connect
client.on_message = on_message

# Kết nối đến MQTT broker
client.connect("mqtt.eclipse.org", 1883, 60)

# Xuất bản tin nhắn
client.publish("home/sensors/temperature", "25.3")

# Bắt đầu vòng lặp để xử lý callback
client.loop_start()
```

## 6. IoT Project Example

Dưới đây là một ví dụ tích hợp của một ứng dụng IoT đơn giản, kết hợp nhiều khái niệm đã học:

```python
import time
import json
import random
from datetime import datetime

# Mô phỏng class cho cảm biến
class Sensor:
    def __init__(self, sensor_id, sensor_type, unit):
        self.sensor_id = sensor_id
        self.sensor_type = sensor_type
        self.unit = unit
        self.is_active = False
    
    def activate(self):
        self.is_active = True
        print(f"Sensor {self.sensor_id} activated")
    
    def deactivate(self):
        self.is_active = False
        print(f"Sensor {self.sensor_id} deactivated")
    
    def read_value(self):
        if not self.is_active:
            return None
        # Các class con sẽ triển khai phương thức này

class TemperatureSensor(Sensor):
    def __init__(self, sensor_id, location):
        super().__init__(sensor_id, "temperature", "°C")
        self.location = location
    
    def read_value(self):
        if not self.is_active:
            return None
        # Mô phỏng đọc giá trị nhiệt độ
        return round(random.uniform(20, 30), 1)

class HumiditySensor(Sensor):
    def __init__(self, sensor_id, location):
        super().__init__(sensor_id, "humidity", "%")
        self.location = location
    
    def read_value(self):
        if not self.is_active:
            return None
        # Mô phỏng đọc giá trị độ ẩm
        return round(random.uniform(40, 80), 1)

# Lớp quản lý thiết bị IoT
class IoTSystem:
    def __init__(self, system_name):
        self.system_name = system_name
        self.sensors = {}
        self.data_log = []
        print(f"IoT System '{system_name}' initialized")
    
    def add_sensor(self, sensor):
        self.sensors[sensor.sensor_id] = sensor
        print(f"Added {sensor.sensor_type} sensor with ID: {sensor.sensor_id}")
    
    def activate_all_sensors(self):
        for sensor_id, sensor in self.sensors.items():
            sensor.activate()
    
    def collect_data(self):
        timestamp = datetime.now().isoformat()
        data_point = {
            "timestamp": timestamp,
            "readings": {}
        }
        
        for sensor_id, sensor in self.sensors.items():
            value = sensor.read_value()
            if value is not None:
                data_point["readings"][sensor_id] = {
                    "type": sensor.sensor_type,
                    "value": value,
                    "unit": sensor.unit
                }
        
        self.data_log.append(data_point)
        return data_point
    
    def get_latest_data(self):
        if not self.data_log:
            return None
        return self.data_log[-1]
    
    def save_data_to_file(self, filename):
        with open(filename, 'w') as f:
            json.dump(self.data_log, f, indent=4)
        print(f"Data saved to {filename}")

# Giả lập IoT Gateway để gửi dữ liệu lên cloud
class IoTGateway:
    def __init__(self, gateway_id, server_url):
        self.gateway_id = gateway_id
        self.server_url = server_url
        print(f"IoT Gateway {gateway_id} initialized, connecting to {server_url}")
    
    def send_data(self, data):
        # Trong thực tế, đây sẽ gửi HTTP request hoặc MQTT message
        print(f"Sending data to {self.server_url}...")
        print(f"Data: {json.dumps(data, indent=2)}")
        # Mô phỏng độ trễ mạng
        time.sleep(0.5)
        print("Data sent successfully")

# Sử dụng các lớp để tạo một ứng dụng IoT đơn giản
def main():
    # Khởi tạo hệ thống IoT
    iot_system = IoTSystem("Home Environment Monitoring")
    
    # Thêm các cảm biến
    temp_living = TemperatureSensor("temp001", "Living Room")
    temp_bedroom = TemperatureSensor("temp002", "Bedroom")
    humidity_living = HumiditySensor("hum001", "Living Room")
    
    iot_system.add_sensor(temp_living)
    iot_system.add_sensor(temp_bedroom)
    iot_system.add_sensor(humidity_living)
    
    # Kích hoạt tất cả cảm biến
    iot_system.activate_all_sensors()
    
    # Khởi tạo Gateway
    gateway = IoTGateway("GW001", "https://iot-cloud-example.com/api/data")
    
    # Thu thập và gửi dữ liệu trong vòng lặp
    print("\nStarting data collection cycle...")
    for i in range(3):  # Mô phỏng 3 chu kỳ đọc dữ liệu
        print(f"\nData collection cycle {i+1}")
        data = iot_system.collect_data()
        gateway.send_data(data)
        time.sleep(2)  # Đợi 2 giây giữa các chu kỳ
    
    # Lưu dữ liệu vào file
    iot_system.save_data_to_file("sensor_data.json")
    
    print("\nSummary:")
    print(f"Total data points collected: {len(iot_system.data_log)}")
    latest = iot_system.get_latest_data()
    print("Latest readings:")
    for sensor_id, reading in latest["readings"].items():
        print(f"  {sensor_id}: {reading['value']} {reading['unit']}")

if __name__ == "__main__":
    main()
```

## Tổng Kết

Trong bài học này, chúng ta đã tìm hiểu về:

1. **Biến (Variables)**: Cách khai báo và sử dụng biến trong Python, các quy tắc đặt tên và phạm vi biến.

2. **Kiểu dữ liệu (Data Types)**:
   - Các kiểu dữ liệu cơ bản: numbers, boolean, string, None
   - Kiểu dữ liệu cấu trúc: list, tuple, dictionary, set
   - Kiểu dữ liệu nâng cao: bytes, bytearray

3. **Hàm và Mô-đun (Functions & Modules)**: Cách định nghĩa và sử dụng hàm, args và kwargs, lambda functions, cách tạo và sử dụng modules và packages.

4. **Lớp và Đối tượng (Classes & Objects)**: Lập trình hướng đối tượng với Python, kế thừa, properties, static methods và class methods.

5. **Import Thư viện Ngoài (External Imports)**: Cách cài đặt và sử dụng các thư viện ngoài, ví dụ với requests, RPi.GPIO và paho.mqtt cho các ứng dụng IoT.

Python là ngôn ngữ linh hoạt và mạnh mẽ, đặc biệt phù hợp cho các dự án IoT. Với kiến thức cơ bản này, bạn có thể bắt đầu phát triển các ứng dụng IoT đơn giản và mở rộng kiến thức theo nhu cầu dự án.

## Bài Tập Thực Hành

1. Viết chương trình đọc dữ liệu từ một cảm biến mô phỏng và lưu vào file CSV.
2. Tạo một class `IoTDevice` với các phương thức để kết nối, gửi dữ liệu và ngắt kết nối.
3. Viết chương trình sử dụng MQTT để xuất bản và đăng ký các thông điệp cảm biến.
4. Tạo một web server đơn giản hiển thị dữ liệu từ các cảm biến (sử dụng Flask hoặc FastAPI).
5. Tạo một dashboard đơn giản để hiển thị dữ liệu cảm biến thời gian thực.
```
