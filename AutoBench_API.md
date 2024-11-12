# API Guide  
## APIs for Initialization  
### ADBInterface.init
init(folder_path: str): int

Initialize the testing platform, set the storage path for result files, and check the ADB environment  

**Parameters：**

| **parameter_name** | **Type** | **Required** | **Description** |
| :---: | :---: | :---: | --- |
| folder_path | str | Y | Test result file storage path, such as the execution paths for successful and failed test cases   |


**Return：**

| **Type** | **Description** |
| :---: | --- |
| int |  0: Initialization successful   -1: ADB environment initialization failed   -2: No permission for result file storage path   -3: Failure due to other reasons   |


## APIs for obtaining task information  
### ADBInterface.get_support_test_task
get_support_test_task(): Dict[str, List[str]]

obtain the supported test content of the platform, including app types and their associated business scenarios

**Return：**

| **Type** | **Description** |
| :---: | --- |
| Dict[str, List[str]] | Returns a dictionary where each key is the name of an app, and the corresponding value is a list of strings containing all test scenarios for that app   |


### ADBInterface.set_test_task
set_test_task(test_content: Dict[str, List[str]]): void

Allow users to independently set the scope of testing, including app types and the business logic within each app  

**Parameters：**

| **parameter_name** | **Type** | **Required** | **Description** |
| :---: | :---: | :---: | --- |
| test_content | Dict[str, List[str]] | Y | A dictionary where each key is the name of an app, and the corresponding value is a list of all user-planned test scenarios within that app   |


### ADBInterface.get_curr_test_task
get_curr_test_task(): Dict[str, str]

Obtain information about the currently ongoing test tasks  

**Return：**

| **Type** | **Description** |
| :---: | --- |
| Dict[str, str] |  Returns the content currently being tested, containing two keys:  <br/>+ `"app_type"`： Represents the app type or name (e.g., 'AppName')  <br/>+ `"scenario"`： Represents the current test scenario (e.g., 'TestScenario')   |


## APIs for obtaining the current app status  
### ADBInterface.get_device_layout
get_device_layout(): str

obtain the layout file of the currently displayed app page  

**Return：**

| **Type** | **Description** |
| :---: | --- |
| str | Returns the layout of the current app page, with the content being the XML structure file of the page converted to a string     |


### ADBInterface.get_device_screenshot
get_device_screenshot(): bytes

 obtain the screenshot information of the currently displayed app page  

**Return：**

| **Type** | **Description** |
| :---: | --- |
| bytes | Returns the screenshot information of the current app page, provided as a binary data stream in `bytes` format     |


## APIs for performing operations  
### ADBInterface.execute_by_coordinates
execute_by_coordinates(x: int, y: int, operation_type: str, input_content(Optional): str): void

Manipulate the current app page based on the horizontal and vertical coordinates  

**Parameters：**

| **parameter_name** | **Type** | **Required** | **Description** |
| :---: | :---: | :---: | :---: |
| x | int | Y |  Widget X-coordinate   |
| y | int | Y |  Widget Y-coordinate   |
| operation_type | str | Y | Manipulation type, currently supported：<br/>"click", "input" |
| input_content | str | N | When the operation type is 'input', specify the content to be entered in this parameter |


### ADBInterface.execute_by_resource_id
execute_by_resource_id(resource_id: int, operation_type: str, input_content(Optional): str): void

**Parameters：**

| **parameter_name** | **Type** | **Required** | **Description** |
| :---: | :---: | :---: | :---: |
| resource_id | int | Y |  Widget resource ID   |
| operation_type | str | Y |  Manipulation type, currently supported：<br/>"click", "input" |
| input_content | str | N |  When the operation type is 'input', specify the content to be entered in this parameter |


### ADBInterface.curr_scenario_finish
curr_scenario_finish(): void

Called when the large model determines that the current test scenario has ended and no further action is needed  

## APIs for obtaining execution results  
### ADBInterface.get_execute_result
get_execute_result(): Dict[str, str]

Obtain the execution result of the current step  

**Return：**

| **Type** | **Description** |
| :---: | --- |
| Dict[str, str] |  Returns a JSON-formatted string with the following elements：<br/>{"curr_task_finished": "True" or "False",<br/> "total_task_finished": "True" or "False",<br/> "curr_execution_result": "True" or "False",<br/> "fail_reason": "True" or "False"}<br/>+ curr_task_finished： Whether the current test scenario end  <br/>+ total_task_finished： Whether all test scenarios have ended, i.e., all tasks mentioned in the nested_list above  <br/>+ curr_execution_result： The result of the current step execution  <br/>+ fail_reason： The failure reason if the current step execution fails   |


## APIs for obtaining the total score  
### ADBInterface.get_final_score
get_final_score(): int

obtain the total score after completing all test tasks  

| **Type** | **Description** |
| :---: | :---: |
| int | Total test score   |


