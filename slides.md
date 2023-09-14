---
theme: default
fonts:
  sans: 'Roboto'
  serif: 'Roboto Slab'
  mono: 'Fira Code'
transition: slide-left
layout: intro
---

# MQTTX & Protobuf ⚡️

<div class="text-lg mt-12">
  <span @click="$slidev.nav.next" class="cursor-pointer text-gray">
    Dive into Publishing and Receiving Protobuf Messages with MQTTX <carbon:arrow-right class="inline"/>
  </span>
</div>

---

# Agenda 📋

- 🖥️ MQTTX Desktop
- 🛠️ MQTTX CLI
- ✅ EMQX Validation

---

<div class="flex flex-col justify-center h-full space-y-4">
  <div class="text-2xl">
    <h1>DEMO 1: MQTTX Desktop 🎬</h1>
  </div>
  <div class="text-lg text-gray">
    Let's explore how MQTTX Desktop can be leveraged for handling Protobuf messages.
  </div>
</div>

---

# Data 📊

```protobuf
syntax = "proto3";
package IoT;

message SensorData {
  string deviceId = 1;
  string sensorType = 2;
  double value = 3;
  int64 timestamp = 4;
}
```

```json
{
  "deviceId": "Device123",
  "sensorType": "Temperature",
  "value": 23.5,
  "timestamp": 1677328490320
}
```

<div class="my-6 text-gray">
  Brief explanation of the Protobuf message structure and JSON message format goes here.
</div>

---

<div class="flex flex-col justify-center h-full space-y-4">
  <div class="text-2xl">
    <h1>DEMO 2: MQTTX CLI 🎬</h1>
  </div>
  <div class="text-lg text-gray">
    We will explore how the MQTTX CLI can be used to work with Protobuf messages.
  </div>
</div>

---

# Data 📊

```protobuf
syntax = "proto3";
package IoT;

message SensorData {
  string deviceId = 1;
  string sensorType = 2;
  double value = 3;
  int64 timestamp = 4;
}
```

<div class="my-6 text-gray">A short explanation on the necessity and utility of defining message schema like above.</div>

---

# Terminal CLI 💻

- Subscribe

```shell
mqttx sub -t 'testtopic/protobuf' -h 127.0.0.1 -Pp ./SensorData.proto -Pmn IoT.SensorData --format json
```

- Publish

```shell
mqttx pub -t 'testtopic/protobuf' -Pp ./SensorData.proto -Pmn IoT.SensorData -h 127.0.0.1 -m '{"deviceId": "Device123", "sensorType": "Temperature", "value": 22.5, "timestamp": 1675873900}'
```

<div class="my-6 text-gray">Here we demonstrate subscribing and publishing messages via MQTTX CLI using the defined Protobuf schema.</div>

---

# EMQX: Validating Protobuf Messages ✅

- Decode

```sql
SELECT
  schema_decode('protobuf_sensor', payload, 'SensorData') as sensor_data, payload
FROM
  "t/#"
```

- Encode

```sql
SELECT
  schema_encode('protobuf_sensor', json_decode(payload), 'SensorData') as protobuf_sensor
FROM
  "t/#"
```

<div class="my-6 text-gray">Using EMQX's schema and rule features, we can effectively validate Protobuf messages</div>

---

<div class="flex flex-col justify-center items-center h-full space-y-4">
  <h1 class="text-2xl font-semibold">
    Thanks 🙏
  </h1>
  <div class="text-lg">
    Feel free to ask any questions.
  </div>
</div>
