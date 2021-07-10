# bang!

Bang is a task runner that uses AWS Lambda to speedup the execution with minimal effort.

You define your task, the input files will be uploaded to S3 for you and the output will also lives there.

## bang init

Creates bang.toml with defult values after asking a few questions.

## bang check

Validate that AWS credentials work, all AWS resources can be created and that the task can be run locally.
Builds the docker container with all the dependencies installed and try to run the task locally.

`--cost`: also shows the estimated cost of execution.

`--profile`: measures necessary memory and edit `bang.toml` accordingly

## bang run

Creates a new execution of the task. Returns immediately after confirming that exeuction started.
Handles upload of files if needed, all AWS resource creation.

## bang monitor

Starts a webserver with a frontend to monitor all executions (inspired on nomad and grok)
Show a taximeter of the costs so far.

## bang download

Download output results from S3

## bang cost

Estimate the cost to run the defined task. Lambda, S3 (input + output)

# .bang folder

Contains the current state of the resources associated with the task.
Metadata about all the exeuctions done so far. Serves as `bang monitor` data backend.

# Cost explosion protection and limits

`bang` will monitor the expected progress of the task and will interrupt the execution if it thinks that it is hung
and would incurr in extra costs. You can configure a limit on the cost and/or execution time.

