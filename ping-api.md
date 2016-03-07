# LoggerDaisy Sensors REST API

**Sending sensor data to LoggerDaisy cloud**

Sensor module sends small 'messages' to API end point with one or more sensor reads. If sensor within the module are not configured from LoggerDaisy Cloud, default sensor reading interval is 30 seconds.

```
POST http://api.loggerdaisy.com/ping
```

Sensor Message format

```
{
	"uid": "sensor-mac-address",
	"module": "LoggerDaisy",
	"version": "2.1",
	"deviceInfo": {
		"heap": 0,
		"majorVer": 0, 
		"minorVer": 0, 
		"devVer":0, 
		"chipid": 0, 
		"flashid": 0, 
		"flashsize": 0, 
		"flashmode": 0, 
		"flashspeed": 0
	}
	"sensors": {
		"temperature": {
			"scale": 1,
			"value": 0.00
		},
		"humidity": {
			"scale": 1,
			"value": 0
		},
		"airpressure": {
			"scale": 1,
			"value": 0
		},
		"c2h4": {
			"scale": 1,
			"value": 0
		}
	}
}
```
**Remarks:**

- _version_ referes to current module design version and it is _2.1_ at this moment
- _firmware_ data can be read via _node.info()_ call

### Configuring Sensor module at run-time

On power up NodeMCU can send a request to LoggerDaisy API for self-configuration before starting reporting sensor data. Each module registered in the cloud has number of sensors that can be configured separately within LoggerDaisy Cloud dashboard.

```
GET http://api.loggerdaisy.com/config/{mac-address}
```

Result

```
{
	"sensors": [
		"temperature": {
			"interval": 10000
		},
		"humidity": {
			"interval": 34800
		}
	]
}
```
