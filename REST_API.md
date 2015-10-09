#IRM 3.2 REST API {#api}


[toc]

##Get list of entities {#entities}
URI
```
/rest/entities
```
Verb		
```
GET
```

Retrieves the list of entities for the currently logged in user

*Sample Returned JSON*
```
{
  "links": [],
  "name": "items",
  "accept": "application/vnd.sas.irm.entity+json,application/vnd.sas.irm.entity+xml",
  "start": null,
  "count": 5,
  "items": [
			{
			"currency": "EUR",
			"parentId": "",
			"baseDate": "12312014",
			"federatedAreaId": "0.2.1",
			"role": {
			"type": 3,
			"name": "GROUP_SOLO",
			"id": "GROUP_SOLO",
			"key": 1,
			"version": 1
			},
  "id": "MAIN",
  "name": "MAIN",
  "key": 319225090,
  "version": 1
  },
  {
  "currency": "EUR",
  "parentId": "main",
  "baseDate": "12312014",
  "federatedAreaId": "0.2.1",
  "role": {
           "type": 1,
           "name": "SOLO",
           "id": "SOLO",
           "key": 1,
           "version": 1
           },
  "id": "ENTITY_BE",
  "name": "ENTITY_BE",
  "key": 484068520,
  "version": 1
  },
  {
  "currency": "EUR",
  "parentId": "main",
  "baseDate": "12312014",
  "federatedAreaId": "0.2.1",
  "role": {
			"type": 2,
			"name": "GROUP",
			"id": "GROUP",
			"key": 1,
			"version": 1
          },
  "id": "REGIONAL_GROUP",
  "name": "REGIONAL_GROUP",
  "key": 2118244664,
  "version": 1
  },
  {
  "currency": "CHF",
  "parentId": "regional_group",
  "baseDate": "12312014",
  "federatedAreaId": "0.2.1",
  "role": {
			"type": 1,
			"name": "SOLO",
			"id": "SOLO",
			"key": 1,
			"version": 1
		  },
  "id": "ENTITY_CH",
  "name": "ENTITY_CH",
  "key": 24790154,
  "version": 1
  },
  {
  "currency": "EUR",
  "parentId": "regional_group",
  "baseDate": "12312014",
  "federatedAreaId": "0.2.1",
  "role": {
			"type": 1,
			"name": "SOLO",
			"id": "SOLO",
			"key": 1,
			"version": 1
		  },
  "id": "ENTITY_IT",
  "name": "ENTITY_IT",
  "key": 123379568,
  "version": 1
  }
  ],
  "limit": null,
  "version": 2
}
```
[Top](#api)

##Get list of base dates {#basedates}

URI		
```
/rest/basedates
```
Verb		
```
GET
```
**Retrieves the list of base dates in the landing area**

*Sample Returned JSON*
```
[
   {
   "name": "12312008",
   "id": "12312008",
   "key": 100
   }
…
]
```
[Top](#api)

##Get list of configuration sets {#configsets}

URI		
```
/rest/configsets
```
Verb		
```
GET
```
**Retrieves the list of base configuration sets loaded by ETL**

*Sample Returned JSON*
```
[
   {
   "name": " SOLVENCY II LEVEL2_OCT2011",
   "id": "SOLVENCY2_LVL2_OCT2011",
   "key": 92312108
   }
…
]
```
[Top](#api)

##Get list of job flow categories {#categories}

URI		
```
/rest/jobflow/categories
```
Verb		
```
GET
```
**Retrieves the list of job flow categories. Note that the list of job flow definitions has a categoryId (which is the long key of one of the categories returned by this method) for each definition. **

*Sample Returned JSON*
```
[
  {
  "entityRoleKey": 1,
  "name": "QRT-ASSETS",
  "id": "QRT-ASSETS",
  "key": 1
  }
  {
  "entityRoleKey": 2,
  "name": "QRT-BASIC",
  "id": "QRT-BASIC",
  "key": 3
  }
]
```
Note: filtering the category list by entity role is not currently supported.
[Top](#api)

##Get list of job flow definitions {#definitions}

URI		
```
/rest/jobflow/definitions?entity={entitykey}
```
Verb		
```
GET
```
**Retrieves the list of job flow definitions **

*Sample Returned JSON*
```
[
  {
  "entityRoleKey": 1,
  "entityKey": 100,
  "url": "jobflow/MarketSolvency.bpmn",
  "categoryKey": 0,
  "name": "MarketSolvency_0",
  "id": "MARKETSOLVENCY",
  "federatedAreaId": "0.2.1",
  "key": 61621557
  },
  {
  "entityRoleKey": 2,"entityKey": 100,
  "url": "jobflow/QRT-ASSETS/S.06.02.a.bpmn",
  "categoryKey": 1,
  "name": "S.06.02.a",
  "id": "S.06.02.A_1",
  "federatedAreaId": "0.2.1",
  "key": 1392859268
  }
]
```
[Top](#api)

##Get a job flow definition {#definition}

URI		
```
/rest/jobflow/definition/{definitionid}
```
Verb		
```
GET
```
**Retrieves the job flow definition whose id is { definitionid } if found. **

*Sample Returned JSON*
```
{
  "fileName": "ARS.bpmn",
  "categoryId": "QRT-ARS",
  "federatedAreaId": "0.3.1",
  "categoryKey": 1364439792,
  "entityRoleKey": 1,
  "frequencyKey": 0,
  "url": "irmcontent/fa.0.3.1/jobflow/QRT-ARS/ARS.bpmn",
  "id": "0.3.1::qrt-ars::ars",
  "name": "Annual Solo (Mkt. Solvency and Op. Risk) Module",
  "key": 1603288271
}
```
[Top](#api)

##Get list of job flow instances information {#instanceinfos}

URI
```
/rest/jobflow/instancesinfos?entity={entitykey}&definition={definitionid}
```
Verb		
```
GET
```

**Retrieves the list of job flow instances information corresponding to the entity identified by {entitykey} and based on the job flow definition whose string id is {definitionid}. An empty array is returned if the list is empty. The entitykey is a long.**

Note	We use the entityKey, which is always unique, in this API because the entity may be coming from different areas and its name/id may not be unique (note that the entityId is being used by base SAS). To simplify the API, we choose to use the entityKey.

Sample Returned JSON

```
[
  {
  "status": 0,
  "jobFlowDefinitionName": "SCR-B3A-QRT-Only",
  "categoryName": "QRT-ASSETS",
  "name": "SCR-B3A-QRT-Only Test Run",
  "description": "This is a sample job flow instance…",
  "baseDate": "12312011",
  "federatedAreaId": "0.2.1",
  "id": "PROCESS_1",
  "key": 1095540298,
  "results": [
				{
				"fileName": "SCR_B3A_AS_DATA.SAS7BDAT",
				"baseName": "SCR_B3A_AS_DATA",
				"version": 0,
				"extension": "SAS7BDAT",
				"url": "pa/data/4986475/CR_B3A_AS_DATA.SAS7BDAT",
				"sourceTask": "_4",
				"libname": "QRTLIB",
				"graphPath": null,
				"name": "QRTLIB.SCR_B3A_AS_DATA.SAS7BDAT",
				"id": "DO_PROCESS_1_4",
				"key": 4986475
				},
				],
  }
]
```
[Top](#api)

##Get a job flow instance information {#instanceinfo}

URI
```
/rest/jobflow/instanceinfos/{instancekey}
```

Verb



##Some math
$$
\int_0^1x^3dx=\frac{x^4}{4} + C
$$
```
GET
```

**Retrieves the job flow instance basic information identified by {instancekey}. An empty object is returned if not found. The instancekey is a long (it’s referred to as the ‘key’ in the returned json). The job flow instance information is much smaller than a job flow instance (see /rest/jobflow/instances/{instancekey}).**

*Sample Returned JSON*
```
Same as above (as an array)
```
[Top](#api)

##Get a job flow instance {#instance}

URI		
```
/rest/jobflow/instances/{instancekey}
```
Verb		
```
GET
```

**Retrieves the job flow instance identified by {instancekey}. An empty object is returned if not found. The instancekey is a long (it’s referred to as the ‘key’ in the returned json). Note that the job flow instance contains can be large. To retrieve basic information (much smaller than a job flow instance) about a job flow instance, use /rest/jobflow/instanceinfos/{instancekey}.**

*Sample Returned JSON*
```
{
	"description": null,
	"jobFlowStatus": 0,
	"entityRoleKey": 1,
	"entityKey": 100,
	"jobFlowDefinitionName": "SCR-B3A-QRT-Only",
	"federatedAreaId": "0.2.1",
	"baseDate": null,
	"tasks": [
	{
	"sasCodePath": "sii_qrt_scr_b3a_as.sas",
	"logFileUrl": "pa/data/4986475/mva_task_1691982872.log",
	"name": "SCR_B3A Adapter",
	"id": "_4",
	"key": 1691982872
	"inputData": [
	{
	"fileName": "CCP_RSK_CAP.SAS7BDAT",
	"baseName": "CCP_RSK_CAP",
	"version": 0,
	"extension": "SAS7BDAT",
	"url": null,
	"sourceTask": null,
	"libname": "MK_CCP",
	"name": "MK_CCP.CCP_RSK_CAP.SAS7BDAT",
	"id": "DO_PROCESS_1_3",
	"key": 843305152
},
	{
	"fileName": "SIM_RES_RPT_L.SAS7BDAT",
	"baseName": "SIM_RES_RPT_L",
	"version": 0,
	"extension": "SAS7BDAT",
	"url": null,
	"sourceTask": null,
	"libname": "MK_VL",
	"graphPath": null,
	"name": "MK_VL.SIM_RES_RPT_L.SAS7BDAT",
	"id": "MK_VL.SIM_RES_RPT_L",
	"key": 122632192
},
	"outputData": [
	{
	"fileName": "SCR_B3A_AS_DATA.SAS7BDAT",
	"baseName": "SCR_B3A_AS_DATA",
	"version": 0,
	"extension": "SAS7BDAT",
	"url": "pa/data/4986475/CR_B3A_AS_DATA.SAS7BDAT",
	"sourceTask": "_4",
	"libname": "QRTLIB",
	"graphPath": null,
	"name": "QRTLIB.SCR_B3A_AS_DATA.SAS7BDAT",
	"id": "DO_PROCESS_1_4",
	"key": 4986475
}
],
},
	"results": [
	{
	"fileName": "SCR_B3A_AS_DATA.SAS7BDAT",
	"baseName": "SCR_B3A_AS_DATA",
	"version": 0,
	"extension": "SAS7BDAT",
	"url": "pa/data/4986475/CR_B3A_AS_DATA.SAS7BDAT",
	"sourceTask": "_4",
	"libname": "QRTLIB",
	"graphPath": null,
	"name": "QRTLIB.SCR_B3A_AS_DATA.SAS7BDAT",
	"id": "DO_PROCESS_1_4",
	"key": 4986475
}
],
	"subFlowInstances": [
	{
	"instanceKey": 817310448,
	"url": "jobflow/Enrichment.bpmn",
	"dataObjects": [ ],
	"tExclusive": true,
	"forCompensation": false,
	"dataInputAssociations": [],
	"dataOutputAssociations": [],
	"implementation": null,
	"executionStatus": "UNKNOWN",
	"asynchronous": false,
	"ioSpecification": null,
	"incomingFlows": [
	{
	"targetRef": "_3",
	"conditionExpression": null,
	"sourceRef": "_2",
	"attributes": { },
	"documentation": null,
	"extensionElements": { },
	"processKey": 1767877100,
	"id": "_4",
	"name": null,
	"key": 839627890
}
	],
	"outgoingFlows": [
	{
	"targetRef": "_5",
	"conditionExpression": null,
	"sourceRef": "_3",
	"attributes": { },
	"documentation": null,
	"extensionElements": { },
	"processKey": 1767877100,
	"id": "_6",
	"name": null,
	"key": 1520744643
}
	],
	"properties": {
	"_3_P_1": {
	"itemSubjectRef": "xsd:string",
	"id": "_3_P_1",
	"name": "path=Enrichment.bpmn",
	"key": 0
}
	},
	"attributes": { },
	"documentation": null,
	"extensionElements": { },
	"processKey": 1630004292,
	"id": "_3",
	"name": "Enrichment",
	"key": 1967244822
}
   ],
      … Details omitted (output too long: external file provided) …
}
```

Notes: 

1.	The “results” node contains copies of the final output generated by the job flow.
2.	If a job flow contains a sub-flow, then, to retrieve the instance data of the sub-flow, use the instanceKey. In the sample above, this instance key is 817310448.
[Top](#api)

##Run a job flow instance {#run}

URI		
```
/rest/jobflow/instances/{instancekey}/run
```

Verb	
```
POST
```

**Executes the job flow instance identified by {instancekey}. Returns an error code (TBD) in case of errors launching the job flow execution. This method returns a running status if the jobflow was launched successfully.**
[Top](#api)

##Create a new job flow instance {#newinstance}

URI		
```
/rest/jobflow/instances
```

Verb
```
POST
```

**Creates a new job flow instance based on passed in parameters (as data in ajax call). Returns the key of the job flow instance created or an error code (TBD) in case of errors.**

**Parameters	name:** the name of the job flow instance to be created
**description:** the description of the job flow instance to be created
**jobFlowDefinitionId:** the id of the job flow file definition 
**federatedAreaId:**  the id of federated area containing the job flow file definition 
**baseDate:** the base date to use (defined in landing area)
**entityId:** the string id of the entity to be used
**entityRoleId:** the id of the entity role to be used
**configSetId:** the id of the configuration set to be used
**categoryId:** the id of the job flow category set to be used


*Sample Arguments;*
```
        var params = {};
        params.name = "SCR-B3A-QRT-Only Instance 1";
        params.description = "This is a test job flow instance...";
        params.jobFlowDefinitionId = "SCR-B3A-QRT-ONLY_2";
        params.federatedAreaId = "0.2.1";
        params.baseDate = "12312011";
        params.entityId = "entity_be";
        params.entityRoleId = "solo";
        params.configSetId = "SOLVENCY2_LVL2_OCT2011";
        params.categoryId = "QRT-ASSETS";
```
 these values are returned in APIs /rest/jobflow/definitions/…  
[Top](#api)

##Get a job flow instance status {#status}

URI
```
/rest/jobflow/instances/{instancekey}/status
```

Verb
```
GET
```

**Retrieves the execution status a job flow instance identified by {instancekey}. An empty object is returned if not found. The instancekey is a long (it’s also referred to as the ‘key’). The job flow instance status consists of its overall execution status (represented by the “jobFlowStatus” in the json output) and the execution status of each its tasks. Each task status consists of the pair “taskKey”:status (see sample json returned). The key is the instance key of the job flow instance.**

*Sample Returned JSON*
```
{
	"key": 1095540298
	"jobFlowStatus": 0,
	"tasksStatus": {
	"1353022261": 0,
	"1058431472": 0
 },
	"subFlowsStatus": {
	"8610026201": 0,
	"2335431400": 0
   }
}
```
[Top](#api)

##Delete a job flow instance {#deleteinstance}

URI
```
/rest/jobflow/instances/{instancekey}
```
Verb
```
DELETE
```

**Deletes the job flow instance identified by {instancekey}. The instancekey is a long (it’s also referred to as the ‘key’). Returns true if successful, false otherwise. **
[Top](#api)

##Cancel a job flow instance run {#cancel}

URI
```
/rest/jobflow/instances/cancel/{instancekey}
```

Verb
```
POST
```

**Cancels the job flow instance execution identified by {instancekey}. The instancekey is a long (it’s also referred to as the ‘key’). Returns true if successful, false otherwise. **
[Top](#api)


##Find job flow instance key {#findkey}

URI
```
/rest/jobflow/instances/findkey?name={instanceName}& definition={bmpnFileName}
& category ={categoryId}& basedate={ basedate }& configset={ configSetId }& entity={ entityId}& entityrole={ entityRoleId}
```

Verb
```
GET
```

**Returns the key job flow instance where:**
**name** = *job flow instance name*
**definition** = *bpmn file name (including extension)*
**category** = *category string id*
**basedate** = *the basedate*
**configset** = *configuration set string id*
**entity** = *entity string id*
**entityrole** = *entity role string id (solo|group|group_solo)*

If the instance is not found, this method returns 0.
[Top](#api)

##Share a job flow instance run {#share}

URI
```
/rest/jobflow/instances/{instancekey}/share
```

Verb
```
POST
```

**Shares the job flow instance (i.e. makes it public and visible to anyone) identified by {instancekey}. Returns the updated jobflow instance info if successful, error otherwise. **
[Top](#api)

##Unshare a job flow instance run {#unshare}

URI
```
/rest/jobflow/instances/{instancekey}/unshare
```

Verb
```
POST
```

**Un-shares the job flow instance (i.e. makes it private and only visible to author) identified by {instancekey}. Returns the updated jobflow instance info if successful, error otherwise. **
[Top](#api)

##Publish a new job flow instance {#publish}

URI
```
/rest/jobflow/instances/{instancekey}/publish
```

Verb		
```
POST
```
**Publishes the job flow instance based on passed in parameters. Returns the job flow instance info of the published instance.**

Parameters	comment: comments to be included in the published instance


*Sample Arguments;*

```
var params = {};
params.comment = "Publishing SCR-B3A-QRT for regulation review.";
```
[Top](#api)

##Find job flow instance key {#findkey}

URI 	           	
```
/rest/jobflow/instances/findkey?name={instanceName}& definition={bmpnFileName}
& category ={categoryId}& basedate={ basedate }& configset={ configSetId }& entity={ entityId}& entityrole={ entityRoleId}
```
Verb		
```
GET
```

**Returns the key job flow instance where:**
**name** = *job flow instance name*
**definition** = *bpmn file name (including extension)*
**category** = *category string id*
**basedate** = *the basedate*
**configset** = *configuration set string id*
**entity** = *entity string id*
**entityrole** = *entity role string id (solo|group|group_solo)*

If the instance is not found, this method returns 0.


##Get job flow messages {#messages}

URI

```
/rest/jobflow/definitions/{definitionid}/messages
```
Verb		
```
GET
```

**Retrieves the list of messages corresponding to the job flow definition whose id is {definitionid}. The definitionid is a string.**

*Sample Returned JSON*
```
{
  "DATA_PREP_TASK": "Data Preparation",
  "MK_RP.SP_SUBRISKAGG_RESULT.SAS7BDAT":    "Sub-Risk Aggregation Results",
…
}
```
##Get global messages

URI		
```
/rest/messages/global
```

Verb		
```
GET
```

**Retrieves the list of global messages as a set of three arrays of messages for [entities](#entities), categories, and job flow names**

*Sample Returned JSON*
```
{
	"entities": [
	{
	"Entity_X": "Some entity",
	"Entity_Y": "Some other entity",
	…
},
	"categories": [
	{
	"Category_X": "Some category",
	"Category_Y": "Some other category",
	…
   },
	"jobflows": [
	{
	"S0.06.02.": "Some QRT",
	…
}
}
```
##Export job flow instance data {#export}

URI 	           	
```
/rest/jobflow/instances/{instancekey}/export/data?data={datakey}&format={format}
```
Verb		
```
GET
```

**Exports task data (either input or output) in job flow instance.**

The *{Instancekey}* identifies the job flow instance. The *{datakey}* identifies the input or output dataset to export. Returns the url of the exported if successful, an error otherwise (TBD). The format argument is optional.  “xlsx” is the only format supported as of the first release.



------



The API will evolve over time. In order to reduce compatibility issues, we document each API in details in section 3… Some API’s will be either deprecated or removed if no longer needed.
2.2 UTF-8 Encoding

All strings passed to and from the mid-tier and server is required to be UTF-8 encoded. For maximum compatibility, normalize to Unicode Normalization Form C (NFC) before UTF-8 encoding.


#2.3 Error Handling

Errors are returned using standard HTTP error code syntax. Any additional info (JSON formatted) is included in the error object (defined next) of the return call. Error codes not listed here are in the REST API methods listed below.

*Error object*
```
{
	    "errorCode": 100,
	    "httpStatusCode": 500
	    "message": "Job flow instance ‘Test’ already exists !",
	    "details": [],
	    "remediation": "",
	    "links": [],
	    "version": 1,
}
```
##Error object description

**errorCode: ** is an internal error code used for localization of server messages (mostly as a result of an exception) on the client. Error codes are described in the RestApiError.java located REST package in the computation server project.
httpStatusCode: is the HTTP error status code
message: is the default error message in the server locale. This message should be used as a default message (in case client fails to locate a localized message corresponding to errorCode)
message: TBD
links: TBD
version: TBD





#2.4 Standard API errors

Code	Description
400	Bad input parameter. Error message should indicate which one and why.
500	Internal server error. 
403	Bad authentication request (wrong user credentials...). 
404	Generic HTTP error. Error message should provide more specific details about the error.
405	Request method not expected (generally should be GET or POST).

