```json
{
	"DevOps/SysTeam": {
		"Pilar": "value Stream",

		"Agile Targets": "Operates with Vision, architecture and UX guidance.",

		"Responsibilites": {
			"Vision": {
				"Quantification": {
					"From User Perspective": {
						"Activation Rate": ">99%",
						"Monthly Mobile App Active Rate": "25%",
						"Monthly Connected Service Active Rate": "50%",
						"Monthly Connected IVI Active Rate": "75%",
						"..."
					},

					"From Business Perspective": {
						"Market Position": "KEEP",
						"Technical Position": "Leading",
						"Additional Annual Revenue": ">2%",
						"Saving Operation Cost": ">30%"
					}

				},


			},

			"architecture": {

				"Function Architecture from Eco-System Perspective": {

					"Target audiences": [
						"Who is our current audience?", 
						"Who is our target audience?",
						"How might that change?",
						"Do they have the same requirements?",
						"How can we find out or work that out?"
					],

					"Operational Readiness": [
						"Availability",
						"Incident",
						"Problem",
						"Knowledge",
						"Event"
					],

					"Data Cost": [
						"hat resource is acceptable for our target audience?",
						"How do they pay for data?",
						"How can we measure that?",
						"Data budgets",
						"Data size and data cost"
					]

				},

				"System Architecture from Engineering Perspective": {

					"Platforms": ["Browsers", "Operating systems", "Hardwares", "How to find out"],

					"Connectivity": ["Cell, wifi, fixed-boardband", "Unreliable, low-bandwidth, capped...", "Offline - onboard?"],

					"Lagency Integration": ["Custom Relationship Management", "Sales", "Manufacturing"]
				}
			},

			"UX guidance": {
				"Products": ["Mobile App", "IVI", "Public Web Portal"],
				"User Context":  [
						["Indoor", "Outdoor"],
						["In home", "At the office", "On the train", "In the car"],
						["Walking", "Siting", "Standing", "driving"],
						["Disracted", "Focus"],
						["Early", "Late", "Morning", "Noon", "Afternoon", "Evening", "Midnight"],
						["Tired", "Stressed", "Exciting", "Desperate"]
					],
				"Requirements vs Implementation": {
					"Performance for different audiences": ["Connectivity and data constraint", "Performance cost"], 
					"Content": {
						"Message Delivery": ["text", "images", "video", "audio", "popup"],
						"Service Delivery": ["vehicle behaviors", "picking up", "help-driving", "education", "spa/massage"],
						"Digtial Products": ["Disucounts/Coupons", "Customized car decoration", "OTA functions"]
					},
					"Functionality": ["Core function", "Nice to have"]
				},
				// How to prioritize them?
			}
		}
	},

	"System Architect": {
		"Pilar": "Program",

		"Agile Targets": "Deliver working, tested full system increments every two weeks."
	}
}

```














## Identify program roles

#### RTE
```json
{
	"DP provides services": [
		"Communication bridge between business and realization", 
		"Demo planning", 
		"Information sharing"],
	"Alignment to a common mission": [
		"Interpret requirements to user stories for sub-systems", 
		"Commitment aournd a clear set of prioritized objectives"]
}

````

#### Executive

#### Product Manager

#### System Architect/UX/Development Manager

## CVMP Planning
PI Planing
======================================================================================================================================
PI4 -> (Huawei contract signed)
    -> Other vendors are still working for PI4

```Input     
{
	Milestone: EL2
	Scope (sub-system): [
	WebPortal, VR, Clean Cabin, Cyber Security, CEA, RC, PSA IT] 
	=> Enabler 
	=> (Difficulties, Priorities)
	=> User stories: As ... I can ... in condition
}
```

```Audit_User_Stories
According to PSA reference
{
	AC1: {
		key:PSA strategy and policy, 
		status: OK},
	AC2: ...                     
	AC3: ...
}
```


###### Before PI5 3 weeks
```Split_use_stories
{
	Counts: 150 - 180,
	Priorites: {
		Optional: >= 20%,
	}
}
```

###### Before PI5 1.5 weeks
```Acceptance_and_Review
By sub-system/feature within 2 days
{
	Best: ...
	Improvable: ...
	Enterprise value: ... (Expect vs Actual)
	Personal value: ... (Expect vs Actual)
}
```

PI5 
======================================================================================================================================

###### PI Planning - the 1st week

```Kick_off
Road map (for this particular PI) - 2 hours
Global architecture Q&A - 2 hours
```

```Release_next_user_stories
{
	Feature 1: ..., 
	Feature 2: ...,
	...,
	Enabler 1: ...,
	Eanbler 2: ...
}
```

```5 enginers * 5 days * 16 weeks = 400 days => - (2 + 3) days = 375 days => Working days during one PI```
```PI_planning_setting the 3rd day
User stories wall
```

```demo the 4th week <- started the 1st Sprint since the 2nd week 
User story acceptance 
Collabration for demo acceptance readiness
```

...... demo for each Sprint

```Preparation_for_next_PI
2 months before next PI -> Features and architecture preparation
                        -> Last call (at least one month for user stories priority alignment)
1 months before next PI -> Requirements confirmation and entering PI preparation
                        -> Full (E2£) function test/validation for current PI
                        -> One A&R before production depolyment
```
PI6
======================================================================================================================================