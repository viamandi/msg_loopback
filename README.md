Spring-boot project to loopback messages at 3s through hivemq broker and save them into postgresql db.

Then the data is read from db and checked against received data.

SW design / Data Flow

Dependency
- postgresql
	- if vehicle_data table is not created then create it
	- data is added from MQTT message payload (VIN, location, etc)
- hivemq mqtt client

Startup
- postgresql
	- VehicleData.java / VehicleDataRepository.java implements hibernate feature
	- if vehicle_data table is not created then create it
	- data is added from MQTT message payload (VIN, location, etc)
- hivemq mqtt client
	- MqttConfig
		- Host / port is hivemq / 1883
		- Topic for subscribe / publish is "listener/new" (for the moment , for simplicity)

Flow
	- At each 3seconds, message is publish with payload
	- subscriber is receiving the data and 