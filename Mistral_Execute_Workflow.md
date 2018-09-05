# Create and execute mistral workflow

## Pre-requisites
* Mistral instance running. Refer this link to setup and run mistral in docker.
* Name of the running mistral container is my_mistral

## Create your first workflow
1. Login to the running mistral container
   ```
   docker exec -it my_mistral bash
   ```
2. Create a directory named workflows (a practice to follow) and create a file named sum_two_num.yaml in it.
   <br/>Copy-paste the contents from this file.
3. Execute below command from the directory workflows to create a workflow
   ```
   mistral workflow-create sum_two_num.yaml
   ```
   The terminal will display the details of the created workflow.
4. This workflow takes two numbers as input and displays the sum. Execute the workflow with below command, terminal will discplay execution details of the workflow.
   ```
   mistral execution-create sum_two_num '{"var1":1 , "var2":2 }'
   ```
5. Take the ID (wf-execution-id) from the output of the step above and check the status of the execution:
   ```
   mistral execution-get <wf-execution-id>
   ```
6. Use below command to list tasks for this execution:
   ```
   mistral task-list <wf-execution-id>
   ```
7. To get the output from individual task use below command:
   ```
   mistral task-get-result <task-id>
   ```

## debug
To run any mistral command in debug add `--debug` to the command