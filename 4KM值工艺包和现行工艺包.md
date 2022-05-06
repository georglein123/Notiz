4K M值工艺包和现行工艺包

用于打印满版实心全颌面牙模

**M值工艺包（波哥最终确定）：**

```c++
{
    "Material": "Model HP 2.0 UV Grey S ",
    "Density": 1.0,
    "MaterialCoeffX": 1.0036000,
    "MaterialCoeffY": 1.0036000,

    "Strategy": {
        "Name": "HD(50um)",
        "Thickness": 50,
		"Offset": 0,
        "LedExposeTime": 1500,
        "LedPower": 21.00,
        "SupportExposeTime": 750,
        "SupportExposePower": 21.00,
        "FirstExposeTime": 3500,
        "FirstExposePower": 21.00,
        "BaseThickness": 1000,
        "BaseStartExposeTime": 3000,
        "BaseEndExposeTime": 1500,
        "ProfileExposeTime": 100,
        "FillExposePower":21.00,
        "FillExposeTime": 1500,
        "PeelMode": 1,

        "MotorParameters": [{
                "MLowerLimit": 0.0,
                "MUpperLimit": 8,
                "Number": 1,
                "WaitTime": 100,
                "Z_AxisUp": [
                    { "v": 400, "s": 300 },
                    { "v": 6000, "s": 2500 },
                    { "v": 6000, "s": 2900 },
                    { "v": 6000, "s": 2900 },
                    { "v": 6000, "s": 2900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -1850 },
                    { "v": 4000, "s": -2850 },
                    { "v": 4000, "s": -2850 },
                    { "v": 4000, "s": -2850 },
                    { "v": 4000, "s": -2850 }
                ]
            },
            {
                "MLowerLimit": 8,
                "MUpperLimit": 10,
                "Number": 2,
                "WaitTime": 200,
                "Z_AxisUp": [
                    { "v": 400, "s": 300 },
                    { "v": 6000, "s": 2500 },
                    { "v": 6000, "s": 2900 },
                    { "v": 6000, "s": 2900 },
                    { "v": 6000, "s": 2900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -1850 },
                    { "v": 4000, "s": -2850 },
                    { "v": 4000, "s": -2850 },
                    { "v": 4000, "s": -2850 },
                    { "v": 4000, "s": -2850 }
                ]
            },
            {
                "MLowerLimit": 10,
                "MUpperLimit": 12,
                "Number": 3,
                "WaitTime": 300,
                "Z_AxisUp": [
                    { "v": 400, "s": 350 },
                    { "v": 6000, "s": 3500 },
                    { "v": 6000, "s": 3900 },
                    { "v": 6000, "s": 3900 },
                    { "v": 6000, "s": 3900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -2850 },
                    { "v": 4000, "s": -3850 },
                    { "v": 4000, "s": -3850 },
                    { "v": 4000, "s": -3850 },
                    { "v": 4000, "s": -3850 }
                ]
            },
            {
                "MLowerLimit": 12,
                "MUpperLimit": 14,
                "Number": 4,
                "WaitTime": 400,
                "Z_AxisUp": [
                    { "v": 400, "s": 350 },
                    { "v": 6000, "s": 3500 },
                    { "v": 6000, "s": 3900 },
                    { "v": 6000, "s": 3900 },
                    { "v": 6000, "s": 3900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -2850 },
                    { "v": 4000, "s": -3850 },
                    { "v": 4000, "s": -3850 },
                    { "v": 2000, "s": -3850 },
                    { "v": 2000, "s": -3850 }
                ]
            },
            {
                "MLowerLimit": 14,
                "MUpperLimit": 16,
                "Number": 5,
                "WaitTime": 500,
                "Z_AxisUp": [
                    { "v": 400, "s": 400 },
                    { "v": 6000, "s": 3500 },
                    { "v": 6000, "s": 4900 },
                    { "v": 6000, "s": 4900 },
                    { "v": 6000, "s": 4900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -2850 },
                    { "v": 4000, "s": -4850 },
                    { "v": 4000, "s": -4850 },
                    { "v": 4000, "s": -4850 },
                    { "v": 4000, "s": -4850 }
                ]
            },
            {
                "MLowerLimit": 16,
                "MUpperLimit": 19,
                "Number": 6,
                "WaitTime": 600,
                "Z_AxisUp": [
                    { "v": 300, "s": 400 },
                    { "v": 6000, "s": 3500 },
                    { "v": 6000, "s": 4900 },
                    { "v": 6000, "s": 4900 },
                    { "v": 6000, "s": 4900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -2850 },
                    { "v": 4000, "s": -4850 },
                    { "v": 4000, "s": -4850 },
                    { "v": 4000, "s": -4850 },
                    { "v": 4000, "s": -4850 }
                ]
            },
            {
                "MLowerLimit": 19,
                "MUpperLimit": 25,
                "Number": 7,
                "WaitTime": 600,
                "Z_AxisUp": [
                    { "v": 300, "s": 900 },
                    { "v": 6000, "s": 3500 },
                    { "v": 6000, "s": 4900 },
                    { "v": 6000, "s": 4900 },
                    { "v": 6000, "s": 4900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -2850 },
                    { "v": 4000, "s": -4850 },
                    { "v": 4000, "s": -4850 },
                    { "v": 4000, "s": -4850 },
                    { "v": 4000, "s": -4850 }
                ]
            },
            {
                "MLowerLimit": 25,
                "MUpperLimit": 30,
                "Number": 8,
                "WaitTime": 1800,
                "Z_AxisUp": [
                    { "v": 300, "s": 650 },
                    { "v": 6000, "s": 3500 },
                    { "v": 6000, "s": 4900 },
                    { "v": 6000, "s": 4900 },
                    { "v": 6000, "s": 4900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -2850 },
                    { "v": 4000, "s": -3850 },
                    { "v": 2000, "s": -4850 },
                    { "v": 2000, "s": -4850 },
                    { "v": 2000, "s": -4850 }
                ]
            },
            {
                "MLowerLimit": 30,
                "MUpperLimit": 35,
                "Number": 9,
                "WaitTime": 2600,
                "Z_AxisUp": [
                    { "v": 300, "s": 650 },
                    { "v": 6000, "s": 3500 },
                    { "v": 6000, "s": 4900 },
                    { "v": 6000, "s": 4900 },
                    { "v": 6000, "s": 4900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -2850 },
                    { "v": 4000, "s": -3850 },
                    { "v": 2000, "s": -4850 },
                    { "v": 2000, "s": -4850 },
                    { "v": 2000, "s": -4850 }
                ]
            },
            {
                "MLowerLimit": 35,
                "MUpperLimit": 42,
                "Number": 10,
                "WaitTime": 3000,
                "Z_AxisUp": [
                    { "v": 300, "s": 700 },
                    { "v": 6000, "s": 3500 },
                    { "v": 6000, "s": 4900 },
                    { "v": 6000, "s": 4900 },
                    { "v": 6000, "s": 4900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -2850 },
                    { "v": 4000, "s": -3850 },
                    { "v": 2000, "s": -4850 },
                    { "v": 2000, "s": -4850 },
                    { "v": 2000, "s": -4850 }
                ]
            },
            {
                "MLowerLimit": 42,
                "MUpperLimit": 60,
                "Number": 11,
                "WaitTime": 4500,
                "Z_AxisUp": [
                    { "v": 300, "s": 700 },
                    { "v": 3000, "s": 1500 },
                    { "v": 6000, "s": 4900 },
                    { "v": 6000, "s": 4900 },
                    { "v": 6000, "s": 4900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -2850 },
                    { "v": 4000, "s": -3850 },
                    { "v": 2000, "s": -4850 },
                    { "v": 2000, "s": -4850 },
                    { "v": 2000, "s": -4850 }
                ]
            },
            {
                "MLowerLimit": 60,
                "MUpperLimit": 90,
                "Number": 12,
                "WaitTime": 7200,
                "Z_AxisUp": [
                    { "v": 300, "s": 1200 },
                    { "v": 3000, "s": 2000 },
                    { "v": 6000, "s": 4900 },
                    { "v": 6000, "s": 4900 },
                    { "v": 6000, "s": 4900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -2850 },
                    { "v": 4000, "s": -3850 },
                    { "v": 2000, "s": -4850 },
                    { "v": 2000, "s": -4850 },
                    { "v": 2000, "s": -4850 }
                ]
            },
            {
                "MLowerLimit": 90,
                "MUpperLimit": 160,
                "Number": 13,
                "WaitTime": 9500,
                "Z_AxisUp": [
                    { "v": 600, "s": 1200 },
                    { "v": 300, "s": 3400 },
                    { "v": 2000, "s": 4400 },
                    { "v": 6000, "s": 12900 },
                    { "v": 6000, "s": 12900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -8850 },
                    { "v": 4000, "s": -10850 },
                    { "v": 2000, "s": -11850 },
                    { "v": 500, "s": -12650 },
                    { "v": 200, "s": -12850 }
                ]
            },
            {
                "MLowerLimit": 160,
                "MUpperLimit": 190,
                "Number": 14,
                "WaitTime": 12100,
                "Z_AxisUp": [
                    { "v": 600, "s": 1800 },
                    { "v": 200, "s": 2400 },
                    { "v": 2000, "s": 3900 },
                    { "v": 6000, "s": 6900 },
                    { "v": 10000, "s": 18900 }
                ],
                "Z_AxisDown": [
                    { "v": 10000, "s": -10850 },
                    { "v": 4000, "s": -16850 },
                    { "v": 2000, "s": -17850 },
                    { "v": 500, "s": -18650 },
                    { "v": 200, "s": -18850 }
                ]
            },
            {
                "MLowerLimit": 190,
                "MUpperLimit": 538,
                "Number": 15,
                "WaitTime": 16000,
                "Z_AxisUp": [
                    { "v": 600, "s": 1000 },
                    { "v": 200, "s": 2400 },
                    { "v": 3000, "s": 3200 },
                    { "v": 10000, "s": 18900 },
                    { "v": 10000, "s": 18900 }
                ],
                "Z_AxisDown": [
                    { "v": 10000, "s": -15850 },
                    { "v": 3000, "s": -17850 },
                    { "v": 300, "s": -18050 },
                    { "v": 200, "s": -18650 },
                    { "v": 100, "s": -18850 }
                ]
            }
        ]
    },
	"DemixContourFill": {
	    "Enable":true,
		"EdgeWidthPix":7,
		"GridLenPix":5,
		"GridOffsetPix":3,
		"JitterPixList":"(4:0)|(4:4)|(0:4)|(0:0)",
		"StepNum":10,
		"AntiPhase":false
	}
}
```

段数：15段

分段区间：0-8，8-10，10-12，12-14，14-16，16-19，19-25，25-30，30-35，35-42，42-60，60-90，90-160，160-190，190-538，



M值工艺包（骏哥确定）

```c++
{
    "Material": "Model HP 2.0 UV Grey S ",
    "Density": 1.0,
    "MaterialCoeffX": 1.0036000,
    "MaterialCoeffY": 1.0036000,

    "Strategy": {
        "Name": "HD(50um)",
        "Thickness": 50,
		"Offset": 0,
        "LedExposeTime": 1500,
        "LedPower": 21.00,
        "SupportExposeTime": 750,
        "SupportExposePower": 21.00,
        "FirstExposeTime": 3500,
        "FirstExposePower": 21.00,
        "BaseThickness": 1000,
        "BaseStartExposeTime": 3000,
        "BaseEndExposeTime": 1500,
        "ProfileExposeTime": 100,
        "FillExposePower":21.00,
        "FillExposeTime": 1500,
        "PeelMode": 1,

        "MotorParameters": [{
                "MLowerLimit": 0.0,
                "MUpperLimit": 8,
                "Number": 1,
                "WaitTime": 100,
                "Z_AxisUp": [
                    { "v": 400, "s": 150 },
                    { "v": 400, "s": 300 },
                    { "v": 400, "s": 450 },
                    { "v": 6000, "s": 2900 },
                    { "v": 6000, "s": 2900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -1850 },
                    { "v": 4000, "s": -2850 },
                    { "v": 4000, "s": -2850 },
                    { "v": 4000, "s": -2850 },
                    { "v": 4000, "s": -2850 }
                ]
            },
            {
                "MLowerLimit": 8,
                "MUpperLimit": 10,
                "Number": 2,
                "WaitTime": 200,
                "Z_AxisUp": [
                    { "v": 400, "s": 150 },
                    { "v": 400, "s": 300 },
                    { "v": 400, "s": 450 },
                    { "v": 6000, "s": 2900 },
                    { "v": 6000, "s": 2900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -1850 },
                    { "v": 4000, "s": -2850 },
                    { "v": 4000, "s": -2850 },
                    { "v": 4000, "s": -2850 },
                    { "v": 4000, "s": -2850 }
                ]
            },
            {
                "MLowerLimit": 10,
                "MUpperLimit": 12,
                "Number": 3,
                "WaitTime": 300,
                "Z_AxisUp": [
                    { "v": 400, "s": 170 },
                    { "v": 400, "s": 350 },
                    { "v": 400, "s": 500 },
                    { "v": 6000, "s": 3900 },
                    { "v": 6000, "s": 3900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -2850 },
                    { "v": 4000, "s": -3850 },
                    { "v": 4000, "s": -3850 },
                    { "v": 4000, "s": -3850 },
                    { "v": 4000, "s": -3850 }
                ]
            },
            {
                "MLowerLimit": 12,
                "MUpperLimit": 14,
                "Number": 4,
                "WaitTime": 400,
                "Z_AxisUp": [
                    { "v": 400, "s": 170 },
                    { "v": 400, "s": 350 },
                    { "v": 400, "s": 500 },
                    { "v": 6000, "s": 3900 },
                    { "v": 6000, "s": 3900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -2850 },
                    { "v": 4000, "s": -3850 },
                    { "v": 4000, "s": -3850 },
                    { "v": 2000, "s": -3850 },
                    { "v": 2000, "s": -3850 }
                ]
            },
            {
                "MLowerLimit": 14,
                "MUpperLimit": 16,
                "Number": 5,
                "WaitTime": 500,
                "Z_AxisUp": [
                    { "v": 300, "s": 200 },
                    { "v": 300, "s": 400 },
                    { "v": 300, "s": 600 },
                    { "v": 6000, "s": 4900 },
                    { "v": 6000, "s": 4900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -2850 },
                    { "v": 4000, "s": -4850 },
                    { "v": 4000, "s": -4850 },
                    { "v": 4000, "s": -4850 },
                    { "v": 4000, "s": -4850 }
                ]
            },
            {
                "MLowerLimit": 16,
                "MUpperLimit": 19,
                "Number": 6,
                "WaitTime": 600,
                "Z_AxisUp": [
                    { "v": 300, "s": 200 },
                    { "v": 300, "s": 400 },
                    { "v": 300, "s": 600 },
                    { "v": 6000, "s": 4900 },
                    { "v": 6000, "s": 4900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -2850 },
                    { "v": 4000, "s": -4850 },
                    { "v": 4000, "s": -4850 },
                    { "v": 4000, "s": -4850 },
                    { "v": 4000, "s": -4850 }
                ]
            },
            {
                "MLowerLimit": 19,
                "MUpperLimit": 25,
                "Number": 7,
                "WaitTime": 600,
                "Z_AxisUp": [
                    { "v": 300, "s": 300 },
                    { "v": 300, "s": 600 },
                    { "v": 300, "s": 900 },
                    { "v": 6000, "s": 4900 },
                    { "v": 6000, "s": 4900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -2850 },
                    { "v": 4000, "s": -4850 },
                    { "v": 4000, "s": -4850 },
                    { "v": 4000, "s": -4850 },
                    { "v": 4000, "s": -4850 }
                ]
            },
            {
                "MLowerLimit": 25,
                "MUpperLimit": 30,
                "Number": 8,
                "WaitTime": 1800,
                "Z_AxisUp": [
                    { "v": 300, "s": 400 },
                    { "v": 300, "s": 650 },
                    { "v": 300, "s": 1000 },
                    { "v": 6000, "s": 4900 },
                    { "v": 6000, "s": 4900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -2850 },
                    { "v": 4000, "s": -3850 },
                    { "v": 2000, "s": -4850 },
                    { "v": 2000, "s": -4850 },
                    { "v": 2000, "s": -4850 }
                ]
            },
            {
                "MLowerLimit": 30,
                "MUpperLimit": 35,
                "Number": 9,
                "WaitTime": 2600,
                "Z_AxisUp": [
                    { "v": 300, "s": 400 },
                    { "v": 300, "s": 650 },
                    { "v": 300, "s": 1000 },
                    { "v": 6000, "s": 4900 },
                    { "v": 6000, "s": 4900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -2850 },
                    { "v": 4000, "s": -3850 },
                    { "v": 2000, "s": -4850 },
                    { "v": 2000, "s": -4850 },
                    { "v": 2000, "s": -4850 }
                ]
            },
            {
                "MLowerLimit": 35,
                "MUpperLimit": 42,
                "Number": 10,
                "WaitTime": 3000,
                "Z_AxisUp": [
                    { "v": 300, "s": 400 },
                    { "v": 300, "s": 700 },
                    { "v": 300, "s": 1100 },
                    { "v": 6000, "s": 4900 },
                    { "v": 6000, "s": 4900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -2850 },
                    { "v": 4000, "s": -3850 },
                    { "v": 2000, "s": -4850 },
                    { "v": 2000, "s": -4850 },
                    { "v": 2000, "s": -4850 }
                ]
            },
            {
                "MLowerLimit": 42,
                "MUpperLimit": 60,
                "Number": 11,
                "WaitTime": 4500,
                "Z_AxisUp": [
                    { "v": 300, "s": 400 },
                    { "v": 300, "s": 700 },
                    { "v": 300, "s": 1100 },
                    { "v": 6000, "s": 4900 },
                    { "v": 6000, "s": 4900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -2850 },
                    { "v": 4000, "s": -3850 },
                    { "v": 2000, "s": -4850 },
                    { "v": 2000, "s": -4850 },
                    { "v": 2000, "s": -4850 }
                ]
            },
            {
                "MLowerLimit": 60,
                "MUpperLimit": 90,
                "Number": 12,
                "WaitTime": 7200,
                "Z_AxisUp": [
                    { "v": 300, "s": 800 },
                    { "v": 300, "s": 1200 },
                    { "v": 300, "s": 1800 },
                    { "v": 6000, "s": 4900 },
                    { "v": 6000, "s": 4900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -2850 },
                    { "v": 4000, "s": -3850 },
                    { "v": 2000, "s": -4850 },
                    { "v": 2000, "s": -4850 },
                    { "v": 2000, "s": -4850 }
                ]
            },
            {
                "MLowerLimit": 90,
                "MUpperLimit": 160,
                "Number": 13,
                "WaitTime": 9500,
                "Z_AxisUp": [
                    { "v": 300, "s": 1600 },
                    { "v": 300, "s": 2400 },
                    { "v": 300, "s": 3600 },
                    { "v": 6000, "s": 12900 },
                    { "v": 6000, "s": 12900 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -12000 },
                    { "v": 500, "s": -12850 },
                    { "v": 500, "s": -12850 },
                    { "v": 500, "s": -12850 },
                    { "v": 500, "s": -12850 }
                ]
            },
            {
                "MLowerLimit": 160,
                "MUpperLimit": 190,
                "Number": 14,
                "WaitTime": 12100,
                "Z_AxisUp": [
                    { "v": 300, "s": 1600 },
                    { "v": 300, "s": 2400 },
                    { "v": 300, "s": 3600 },
                    { "v": 6000, "s": 6900 },
                    { "v": 10000, "s": 18900 }
                ],
                "Z_AxisDown": [
                    { "v": 10000, "s": -18000 },
                    { "v": 500, "s": -18850 },
                    { "v": 500, "s": -18850 },
                    { "v": 500, "s": -18850 },
                    { "v": 500, "s": -18850 }
                ]
            },
            {
                "MLowerLimit": 190,
                "MUpperLimit": 538,
                "Number": 15,
                "WaitTime": 16000,
                "Z_AxisUp": [
                    { "v": 200, "s": 1600 },
                    { "v": 200, "s": 2400 },
                    { "v": 200, "s": 3600 },
                    { "v": 10000, "s": 18900 },
                    { "v": 10000, "s": 18900 }
                ],
                "Z_AxisDown": [
                    { "v": 10000, "s": -18000 },
                    { "v": 500, "s": -18850 },
                    { "v": 500, "s": -18850 },
                    { "v": 500, "s": -18850 },
                    { "v": 500, "s": -18850 }
                ]
            }
        ]
    },
	"DemixContourFill": {
	    "Enable":true,
		"EdgeWidthPix":7,
		"GridLenPix":5,
		"GridOffsetPix":3,
		"JitterPixList":"(4:0)|(4:4)|(0:4)|(0:0)",
		"StepNum":10,
		"AntiPhase":false
	}
}
```



**现行工艺包：13_Model HP 2.0 UV Grey Solid_50_E&P**

```c++
{
    "Material": "Model HP 2.0 UV Grey Solid",
    "Density": 1.0,
    "MaterialCoeffX": 1.0036000,
    "MaterialCoeffY": 1.0036000,

    "Strategy": {
        "Name": "HD(50um)",
        "Thickness": 50,
        "Offset": 0,
        "LedExposeTime": 1500,
        "LedPower": 21.00,
        "SupportExposeTime": 750,
        "SupportExposePower": 21.00,
        "FirstExposeTime": 3500,
        "FirstExposePower": 21.00,
        "BaseThickness": 1000,
        "BaseStartExposeTime": 3000,
        "BaseEndExposeTime": 1500,
        "ProfileExposeTime": 100,
        "FillExposePower":21.00,
        "FillExposeTime": 1500,
        "PeelMode": 1,

        "MotorParameters": [{
                "AreaLowerLimit": 0.0,
                "AreaUpperLimit": 10.0,
                "Number": 1,
                "WaitTime": 2000,
                "Z_AxisUp": [
                    { "v": 350, "s": 500 },
                    { "v": 350, "s": 750 },
                    { "v": 350, "s": 1100 },
                    { "v": 6000, "s": 5500 },
                    { "v": 6000, "s": 5500 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -4000 },
                    { "v": 2000, "s": -5450 },
                    { "v": 2000, "s": -5450 },
                    { "v": 2000, "s": -5450 },
                    { "v": 2000, "s": -5450 }
                ]
            },
            {
                "AreaLowerLimit": 10.0,
                "AreaUpperLimit": 30.0,
                "Number": 2,
                "WaitTime": 4000,
                "Z_AxisUp": [
                    { "v": 300, "s": 650 },
                    { "v": 300, "s": 950 },
                    { "v": 300, "s": 1400 },
                    { "v": 6000, "s": 6500 },
                    { "v": 6000, "s": 6500 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -5000 },
                    { "v": 2000, "s": -6450 },
                    { "v": 2000, "s": -6450 },
                    { "v": 2000, "s": -6450 },
                    { "v": 2000, "s": -6450 }
                ]
            },
            {
                "AreaLowerLimit": 30.0,
                "AreaUpperLimit": 50.0,
                "Number": 3,
                "WaitTime": 7500,
                "Z_AxisUp": [
                    { "v": 300, "s": 800 },
                    { "v": 300, "s": 1200 },
                    { "v": 300, "s": 1800 },
                    { "v": 6000, "s": 7000 },
                    { "v": 6000, "s": 7000 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -6000 },
                    { "v": 2000, "s": -6950 },
                    { "v": 2000, "s": -6950 },
                    { "v": 2000, "s": -6950 },
                    { "v": 2000, "s": -6950 }
                ]
            },
            {
                "AreaLowerLimit": 50.0,
                "AreaUpperLimit": 100.0,
                "Number": 4,
                "WaitTime": 10000,
                "Z_AxisUp": [
                    { "v": 200, "s": 1200 },
                    { "v": 200, "s": 1800 },
                    { "v": 200, "s": 2500 },
                    { "v": 6000, "s": 7000 },
                    { "v": 6000, "s": 7000 }
                ],
                "Z_AxisDown": [
                    { "v": 6000, "s": -6000 },
                    { "v": 500, "s": -6950 },
                    { "v": 500, "s": -6950 },
                    { "v": 500, "s": -6950 },
                    { "v": 500, "s": -6950 }
                ]
            }
        ]
    },
	"DemixContourFill": {
	    "Enable":true,
		"EdgeWidthPix":7,
		"GridLenPix":5,
		"GridOffsetPix":3,
		"JitterPixList":"(4:0)|(4:4)|(0:4)|(0:0)",
		"StepNum":10,
		"AntiPhase":false
	}
}
```

