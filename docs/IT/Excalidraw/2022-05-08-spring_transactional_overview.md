---

excalidraw-plugin: parsed
tags: [excalidraw]

---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠==


# Text Elements
UserContoller

@Autowired
UserService userDervice; ^0BKucvKL

@Tranactional
UserService proxy

1. txManager.getTransaction()

2. userService.registerUser()

3. txManager.commit() ^SX1fmMFQ

DataSOurceTransactionManager

dataSource.getConnection();
autoCommit(fasle);
bindResource(dataSource, connection);


connection.commit();
afterCommit(); ^Vho8aiaa

TransactionSynchronizationManager

ThreadLocal<Map<Object, Object>> resources

ThreadLocal<Set<TransactionSynchronization>> synchronizations ^itJGcNfz

TransactionManager ^lvDvv7ug

JDBC DriverManager / Pool ^Ccx8am8Q

Database ^aFXRzAhH

%%
# Drawing
```json
{
	"type": "excalidraw",
	"version": 2,
	"source": "https://excalidraw.com",
	"elements": [
		{
			"type": "rectangle",
			"version": 558,
			"versionNonce": 890277652,
			"isDeleted": false,
			"id": "xC2yOT1B1iUGSFDSpgi3W",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -425.84634608314155,
			"y": -599.8771718343099,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 217,
			"height": 99,
			"seed": 1984917292,
			"groupIds": [],
			"strokeSharpness": "sharp",
			"boundElements": [
				{
					"type": "text",
					"id": "0BKucvKL"
				},
				{
					"id": "kZe1QR8OsCGV9XEAZab63",
					"type": "arrow"
				}
			],
			"updated": 1652018746514,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 617,
			"versionNonce": 164326192,
			"isDeleted": false,
			"id": "0BKucvKL",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -420.84634608314155,
			"y": -594.8771718343099,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 207,
			"height": 76,
			"seed": 133543212,
			"groupIds": [],
			"strokeSharpness": "sharp",
			"boundElements": [],
			"updated": 1653207078554,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 2,
			"text": "UserContoller\n\n@Autowired\nUserService userDervice;",
			"rawText": "UserContoller\n\n@Autowired\nUserService userDervice;",
			"baseline": 72,
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": "xC2yOT1B1iUGSFDSpgi3W",
			"originalText": "UserContoller\n\n@Autowired\nUserService userDervice;"
		},
		{
			"type": "rectangle",
			"version": 384,
			"versionNonce": 1540721812,
			"isDeleted": false,
			"id": "LepykMAXVExE9pPjFM1pc",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -438.72055912017817,
			"y": -436.25147774105983,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 266,
			"height": 182,
			"seed": 906313388,
			"groupIds": [],
			"strokeSharpness": "sharp",
			"boundElements": [
				{
					"type": "text",
					"id": "SX1fmMFQ"
				}
			],
			"updated": 1652018746514,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 441,
			"versionNonce": 1532501968,
			"isDeleted": false,
			"id": "SX1fmMFQ",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -433.72055912017817,
			"y": -431.25147774105983,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 256,
			"height": 152,
			"seed": 22980500,
			"groupIds": [],
			"strokeSharpness": "sharp",
			"boundElements": [],
			"updated": 1653207078555,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 2,
			"text": "@Tranactional\nUserService proxy\n\n1. txManager.getTransaction()\n\n2. userService.registerUser()\n\n3. txManager.commit()",
			"rawText": "@Tranactional\nUserService proxy\n\n1. txManager.getTransaction()\n\n2. userService.registerUser()\n\n3. txManager.commit()",
			"baseline": 148,
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": "LepykMAXVExE9pPjFM1pc",
			"originalText": "@Tranactional\nUserService proxy\n\n1. txManager.getTransaction()\n\n2. userService.registerUser()\n\n3. txManager.commit()"
		},
		{
			"type": "rectangle",
			"version": 674,
			"versionNonce": 740219412,
			"isDeleted": false,
			"id": "VqK4xtlw-U6ielTTwNPQo",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -63.4106821786786,
			"y": -440.3456531706311,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 339,
			"height": 194,
			"seed": 1018539180,
			"groupIds": [],
			"strokeSharpness": "sharp",
			"boundElements": [
				{
					"type": "text",
					"id": "Vho8aiaa"
				},
				{
					"id": "Qx7YL11jj_5OEQXKcyLUy",
					"type": "arrow"
				},
				{
					"id": "YeEKV5_oyiaVBHdegJLka",
					"type": "arrow"
				},
				{
					"id": "rwOmCSMuuFkEKq7zftUE-",
					"type": "arrow"
				},
				{
					"id": "iCliowybZcQ9FLfVeIi54",
					"type": "arrow"
				}
			],
			"updated": 1652018746514,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 810,
			"versionNonce": 983676880,
			"isDeleted": false,
			"id": "Vho8aiaa",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -58.4106821786786,
			"y": -435.3456531706311,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 329,
			"height": 171,
			"seed": 1826650516,
			"groupIds": [],
			"strokeSharpness": "sharp",
			"boundElements": [],
			"updated": 1653207078560,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 2,
			"text": "DataSOurceTransactionManager\n\ndataSource.getConnection();\nautoCommit(fasle);\nbindResource(dataSource, connection);\n\n\nconnection.commit();\nafterCommit();",
			"rawText": "DataSOurceTransactionManager\n\ndataSource.getConnection();\nautoCommit(fasle);\nbindResource(dataSource, connection);\n\n\nconnection.commit();\nafterCommit();",
			"baseline": 167,
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": "VqK4xtlw-U6ielTTwNPQo",
			"originalText": "DataSOurceTransactionManager\n\ndataSource.getConnection();\nautoCommit(fasle);\nbindResource(dataSource, connection);\n\n\nconnection.commit();\nafterCommit();"
		},
		{
			"type": "rectangle",
			"version": 615,
			"versionNonce": 283277204,
			"isDeleted": false,
			"id": "viUh-toUawV6CPs6Ittz5",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -184.6740545737439,
			"y": -167.81656699826863,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 516,
			"height": 105,
			"seed": 54984492,
			"groupIds": [],
			"strokeSharpness": "sharp",
			"boundElements": [
				{
					"type": "text",
					"id": "itJGcNfz"
				},
				{
					"id": "Qx7YL11jj_5OEQXKcyLUy",
					"type": "arrow"
				},
				{
					"id": "YeEKV5_oyiaVBHdegJLka",
					"type": "arrow"
				}
			],
			"updated": 1652018746514,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 576,
			"versionNonce": 505209136,
			"isDeleted": false,
			"id": "itJGcNfz",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -179.6740545737439,
			"y": -162.81656699826863,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 506,
			"height": 95,
			"seed": 1734617620,
			"groupIds": [],
			"strokeSharpness": "sharp",
			"boundElements": [],
			"updated": 1653207078563,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 2,
			"text": "TransactionSynchronizationManager\n\nThreadLocal<Map<Object, Object>> resources\n\nThreadLocal<Set<TransactionSynchronization>> synchronizations",
			"rawText": "TransactionSynchronizationManager\n\nThreadLocal<Map<Object, Object>> resources\n\nThreadLocal<Set<TransactionSynchronization>> synchronizations",
			"baseline": 91,
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": "viUh-toUawV6CPs6Ittz5",
			"originalText": "TransactionSynchronizationManager\n\nThreadLocal<Map<Object, Object>> resources\n\nThreadLocal<Set<TransactionSynchronization>> synchronizations"
		},
		{
			"type": "arrow",
			"version": 46,
			"versionNonce": 1230232016,
			"isDeleted": false,
			"id": "kZe1QR8OsCGV9XEAZab63",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -356.0973934087999,
			"y": -499.87717183430993,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 0,
			"height": 64.17592494391715,
			"seed": 1279645076,
			"groupIds": [],
			"strokeSharpness": "round",
			"boundElements": [],
			"updated": 1653207078553,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "xC2yOT1B1iUGSFDSpgi3W",
				"gap": 1,
				"focus": 0.3571525099139019
			},
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					0,
					64.17592494391715
				]
			]
		},
		{
			"type": "arrow",
			"version": 39,
			"versionNonce": 1551705644,
			"isDeleted": false,
			"id": "gUW3ygcoWvJXm5Q9Rl28q",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -214.6283643909428,
			"y": -364.3407732575803,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 157.74396623883933,
			"height": 15.02328055245539,
			"seed": 691644204,
			"groupIds": [],
			"strokeSharpness": "round",
			"boundElements": [],
			"updated": 1652018746515,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					157.74396623883933,
					-15.02328055245539
				]
			]
		},
		{
			"type": "arrow",
			"version": 59,
			"versionNonce": 1664761296,
			"isDeleted": false,
			"id": "Qx7YL11jj_5OEQXKcyLUy",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 185.99157841039647,
			"y": -244.15483401371876,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 1.251743861607224,
			"height": 75.11631556919644,
			"seed": 699924652,
			"groupIds": [],
			"strokeSharpness": "round",
			"boundElements": [],
			"updated": 1653207078561,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "VqK4xtlw-U6ielTTwNPQo",
				"gap": 2.1908191569123687,
				"focus": -0.4572871475727702
			},
			"endBinding": {
				"elementId": "viUh-toUawV6CPs6Ittz5",
				"gap": 1.2219514462536836,
				"focus": 0.44350618559600086
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					1.251743861607224,
					75.11631556919644
				]
			]
		},
		{
			"type": "arrow",
			"version": 72,
			"versionNonce": 852624336,
			"isDeleted": false,
			"id": "YeEKV5_oyiaVBHdegJLka",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 4.922220029406091,
			"y": -172.6240449446365,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 0.4615777239203558,
			"height": 71.53078906908226,
			"seed": 733557548,
			"groupIds": [],
			"strokeSharpness": "round",
			"boundElements": [],
			"updated": 1653207078562,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "viUh-toUawV6CPs6Ittz5",
				"gap": 4.807477946367868,
				"focus": -0.2633515958507347
			},
			"endBinding": {
				"elementId": "VqK4xtlw-U6ielTTwNPQo",
				"gap": 2.1908191569123687,
				"focus": 0.60113553108882
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					-0.4615777239203558,
					-71.53078906908226
				]
			]
		},
		{
			"type": "line",
			"version": 53,
			"versionNonce": 1516711956,
			"isDeleted": false,
			"id": "Fqnv1ZKOJmX9vtYxz41zF",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -424.9539433529963,
			"y": -570.9104230901694,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 217.8370884486606,
			"height": 1.2518746512275811,
			"seed": 1688505644,
			"groupIds": [],
			"strokeSharpness": "round",
			"boundElements": [],
			"updated": 1652018746515,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": null,
			"points": [
				[
					0,
					0
				],
				[
					217.8370884486606,
					1.2518746512275811
				]
			]
		},
		{
			"type": "line",
			"version": 72,
			"versionNonce": 1190300460,
			"isDeleted": false,
			"id": "0z1uXofVrQMTkjAXcRyhC",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -439.977311098532,
			"y": -388.1276123340311,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 269.1667829241071,
			"height": 0,
			"seed": 1032744492,
			"groupIds": [],
			"strokeSharpness": "round",
			"boundElements": [],
			"updated": 1652018746515,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": null,
			"points": [
				[
					0,
					0
				],
				[
					269.1667829241071,
					0
				]
			]
		},
		{
			"type": "line",
			"version": 42,
			"versionNonce": 1068502420,
			"isDeleted": false,
			"id": "nl6sfKy3Dfb7FnZy_tjPv",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -61.892245529335696,
			"y": -410.6624895661739,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 339.2750767299108,
			"height": 1.2519182477678328,
			"seed": 183033260,
			"groupIds": [],
			"strokeSharpness": "round",
			"boundElements": [],
			"updated": 1652018746515,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": null,
			"points": [
				[
					0,
					0
				],
				[
					339.2750767299108,
					1.2519182477678328
				]
			]
		},
		{
			"type": "line",
			"version": 57,
			"versionNonce": 1565541804,
			"isDeleted": false,
			"id": "aIZk18kMm_TrMBK715yw-",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -183.32988503826425,
			"y": -133.98437154162036,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 515.7979910714286,
			"height": 2.5038364955357792,
			"seed": 1226526996,
			"groupIds": [],
			"strokeSharpness": "round",
			"boundElements": [],
			"updated": 1652018746515,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": null,
			"points": [
				[
					0,
					0
				],
				[
					515.7979910714286,
					-2.5038364955357792
				]
			]
		},
		{
			"type": "rectangle",
			"version": 84,
			"versionNonce": 318847764,
			"isDeleted": false,
			"id": "GEJotlcy3K8dqg2GeXZX2",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -65.64800027263925,
			"y": -485.7786743457498,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 342,
			"height": 43.817792619977695,
			"seed": 619161748,
			"groupIds": [],
			"strokeSharpness": "sharp",
			"boundElements": [
				{
					"type": "text",
					"id": "lvDvv7ug"
				}
			],
			"updated": 1652018746515,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 10,
			"versionNonce": 85110828,
			"isDeleted": false,
			"id": "lvDvv7ug",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -60.64800027263925,
			"y": -480.7786743457498,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 332,
			"height": 19,
			"seed": 473570604,
			"groupIds": [],
			"strokeSharpness": "sharp",
			"boundElements": [],
			"updated": 1652018746515,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 2,
			"text": "TransactionManager",
			"rawText": "TransactionManager",
			"baseline": 15,
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": "GEJotlcy3K8dqg2GeXZX2",
			"originalText": "TransactionManager"
		},
		{
			"type": "diamond",
			"version": 36,
			"versionNonce": 248559764,
			"isDeleted": false,
			"id": "e4H3fkbXStbWF6j0Xtdqq",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 211.03011775191442,
			"y": -459.48804237030345,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 33.802490234375114,
			"height": 38.81003243582592,
			"seed": 1985228972,
			"groupIds": [],
			"strokeSharpness": "sharp",
			"boundElements": [],
			"updated": 1652018746515,
			"link": null,
			"locked": false
		},
		{
			"type": "arrow",
			"version": 91,
			"versionNonce": 237226668,
			"isDeleted": false,
			"id": "yK4_kqTBt70XuZdDO-M76",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -260.950211489157,
			"y": -285.46879013816056,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 200.30988420758922,
			"height": 3.755841936383945,
			"seed": 1229671316,
			"groupIds": [],
			"strokeSharpness": "round",
			"boundElements": [],
			"updated": 1652018746515,
			"link": null,
			"locked": false,
			"startBinding": null,
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					200.30988420758922,
					3.755841936383945
				]
			]
		},
		{
			"type": "rectangle",
			"version": 68,
			"versionNonce": 785679892,
			"isDeleted": false,
			"id": "WaJSWs_min72rlf3SZDPx",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 334.0606004528072,
			"y": -415.6701625572454,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 166,
			"height": 74,
			"seed": 112843564,
			"groupIds": [],
			"strokeSharpness": "sharp",
			"boundElements": [
				{
					"type": "text",
					"id": "Ccx8am8Q"
				},
				{
					"id": "iCliowybZcQ9FLfVeIi54",
					"type": "arrow"
				},
				{
					"id": "Cl753SiO7r46dIiosY10T",
					"type": "arrow"
				},
				{
					"id": "klaeUGfbAO9yQwTrAbWEU",
					"type": "arrow"
				}
			],
			"updated": 1652018746515,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 81,
			"versionNonce": 1580740400,
			"isDeleted": false,
			"id": "Ccx8am8Q",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 339.0606004528072,
			"y": -397.6701625572454,
			"strokeColor": "#000000",
			"backgroundColor": "#ced4da",
			"width": 156,
			"height": 38,
			"seed": 1296334740,
			"groupIds": [],
			"strokeSharpness": "sharp",
			"boundElements": [],
			"updated": 1653207078567,
			"link": null,
			"locked": false,
			"fontSize": 16,
			"fontFamily": 2,
			"text": "JDBC DriverManager\n/ Pool",
			"rawText": "JDBC DriverManager / Pool",
			"baseline": 34,
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "WaJSWs_min72rlf3SZDPx",
			"originalText": "JDBC DriverManager / Pool"
		},
		{
			"type": "ellipse",
			"version": 358,
			"versionNonce": 134390676,
			"isDeleted": false,
			"id": "zr6Sg8InpEhKMMf2DMcFp",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 558.1576289126288,
			"y": -425.6858137151694,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 110.17037527901778,
			"height": 105.16270228794644,
			"seed": 668985876,
			"groupIds": [],
			"strokeSharpness": "sharp",
			"boundElements": [
				{
					"type": "text",
					"id": "aFXRzAhH"
				},
				{
					"id": "klaeUGfbAO9yQwTrAbWEU",
					"type": "arrow"
				}
			],
			"updated": 1652018746515,
			"link": null,
			"locked": false
		},
		{
			"type": "arrow",
			"version": 39,
			"versionNonce": 2017130800,
			"isDeleted": false,
			"id": "rwOmCSMuuFkEKq7zftUE-",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 279.989497402212,
			"y": -385.74665995307873,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 56.33719308035711,
			"height": 1.2519182477678328,
			"seed": 36260780,
			"groupIds": [],
			"strokeSharpness": "round",
			"boundElements": [],
			"updated": 1653207078558,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "VqK4xtlw-U6ielTTwNPQo",
				"gap": 4.400179580890608,
				"focus": -0.38243440739717566
			},
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					56.33719308035711,
					-1.2519182477678328
				]
			]
		},
		{
			"type": "arrow",
			"version": 33,
			"versionNonce": 1950956336,
			"isDeleted": false,
			"id": "iCliowybZcQ9FLfVeIi54",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 332.5707613531048,
			"y": -364.4637445652439,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 55.981443531783384,
			"height": 0,
			"seed": 970336916,
			"groupIds": [],
			"strokeSharpness": "round",
			"boundElements": [],
			"updated": 1653207078565,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "WaJSWs_min72rlf3SZDPx",
				"gap": 1.489839099702408,
				"focus": -0.3839572430270673
			},
			"endBinding": {
				"elementId": "VqK4xtlw-U6ielTTwNPQo",
				"gap": 1,
				"focus": -0.21771228241868879
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					-55.981443531783384,
					0
				]
			]
		},
		{
			"type": "text",
			"version": 36,
			"versionNonce": 965949996,
			"isDeleted": false,
			"id": "aFXRzAhH",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 563.1576289126288,
			"y": -382.60446257119617,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 100.17037527901778,
			"height": 19,
			"seed": 1280333484,
			"groupIds": [],
			"strokeSharpness": "sharp",
			"boundElements": [],
			"updated": 1652018746515,
			"link": null,
			"locked": false,
			"fontSize": 16.027260044642844,
			"fontFamily": 2,
			"text": "Database",
			"rawText": "Database",
			"baseline": 15,
			"textAlign": "center",
			"verticalAlign": "middle",
			"containerId": "zr6Sg8InpEhKMMf2DMcFp",
			"originalText": "Database"
		},
		{
			"type": "arrow",
			"version": 32,
			"versionNonce": 1012879312,
			"isDeleted": false,
			"id": "Cl753SiO7r46dIiosY10T",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 505.33826972364056,
			"y": -386.99857820084657,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 56.337018694196445,
			"height": 2.503923688616055,
			"seed": 366712364,
			"groupIds": [],
			"strokeSharpness": "round",
			"boundElements": [],
			"updated": 1653207078565,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "WaJSWs_min72rlf3SZDPx",
				"gap": 5.277669270833371,
				"focus": -0.10825723643978188
			},
			"endBinding": null,
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					56.337018694196445,
					-2.503923688616055
				]
			]
		},
		{
			"type": "arrow",
			"version": 34,
			"versionNonce": 1875560752,
			"isDeleted": false,
			"id": "klaeUGfbAO9yQwTrAbWEU",
			"fillStyle": "solid",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 556.667524062499,
			"y": -363.2118283425207,
			"strokeColor": "#000000",
			"backgroundColor": "transparent",
			"width": 51.32925433885839,
			"height": 1.2520074658929161,
			"seed": 362484652,
			"groupIds": [],
			"strokeSharpness": "round",
			"boundElements": [],
			"updated": 1653207078568,
			"link": null,
			"locked": false,
			"startBinding": {
				"elementId": "zr6Sg8InpEhKMMf2DMcFp",
				"gap": 2.4277640140765726,
				"focus": -0.16184234414790982
			},
			"endBinding": {
				"elementId": "WaJSWs_min72rlf3SZDPx",
				"gap": 5.277669270833371,
				"focus": 0.48337783834499776
			},
			"lastCommittedPoint": null,
			"startArrowhead": null,
			"endArrowhead": "arrow",
			"points": [
				[
					0,
					0
				],
				[
					-51.32925433885839,
					1.2520074658929161
				]
			]
		}
	],
	"appState": {
		"theme": "light",
		"viewBackgroundColor": "#ffffff",
		"currentItemStrokeColor": "#000000",
		"currentItemBackgroundColor": "transparent",
		"currentItemFillStyle": "solid",
		"currentItemStrokeWidth": 1,
		"currentItemStrokeStyle": "solid",
		"currentItemRoughness": 1,
		"currentItemOpacity": 100,
		"currentItemFontFamily": 2,
		"currentItemFontSize": 16,
		"currentItemTextAlign": "left",
		"currentItemStrokeSharpness": "sharp",
		"currentItemStartArrowhead": null,
		"currentItemEndArrowhead": "arrow",
		"currentItemLinearStrokeSharpness": "round",
		"gridSize": null,
		"colorPalette": {}
	},
	"files": {}
}
```
%%