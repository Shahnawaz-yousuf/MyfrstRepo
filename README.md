Project_Name:   "AWS Cloud Cost Optimization - Identifying Stale Resources"
==================================================================================


=> Where "Stale Resources stands for those resources that we dont need to keep but it is generating bills."

==================================================================================

=> Identifying Stale EBS Snapshots:
In this example, we'll create a Lambda function that identifies EBS snapshots that are no longer associated with any active EC2 instance and deletes them to save on storage costs.

=> Mthodology: Here in we use the following steps to achive this project:

Step-1: Go to AWS Managment Console => IAM Role => Create a role for Lambda function (Rolename - "LambdaCostOptimizationrole") => Now select the Policies => search for "AWSLambdaBasicExecutionRole-4878a2e8-aa16-47" attach it with you created role.

Step-2: Now create one policy => select EC2 => Action Allowed => search for (i) DescribeInstance and select (ii) DescribeVolume and select and create the policy with name - like something (EC2-Lambda-policy)

Step-3: Now create one policy => select EC2 => Action Allowed => search for (i) Describesnapshot and select (ii) Deletesnapshot and select and create the policy with name - like something (stale-snapshot-policy)

Step-4: Attach all above two policies with the created Lambda role.

Step-5: Go to Lambda Service => Create Lambda function(any_name) and select the existing role "LambdaCostOptimizationrole" while creating the Lambda Function.

Step-6: Now Go to created Lambda function => Configurations => General Configuration => and Edit the execution time to 10s.

Step-7: Now on the code page just copy the Python code shared here. => Deploy

Step-8: Now Launch one (OR MORE) EC2 instance in the same region and create the snapshot attached with the volume of that instance.

Step-9: On lambda Function click on TEST => Give the name of the event (anyname: test)

Step-10: Now try to execute the code by manualling triggering Lambda => click on: TEST and wait

Step-11: On the same dashboard Lambda will execute successfully the code but the snapshot will not get deleted (just can cross check on console) because it is already attached with a running instance and attached live volume.

Step-12: Now Terminate the Instance that will delete the volume automatically as usual. But the snapshot will not get deleted and will remain there. (i.e, stale snapshot)

Step-13: Now Again execute the code via Lambda function and check the snapshot(s) got deleted or not.

=> Result - Stale snapshot will be deleted now. hence project is successfull.

=> Description:
The Lambda function fetches all EBS snapshots owned by the same account ('self') and also retrieves a list of active EC2 instances (running and stopped). For each snapshot, it checks if the associated volume (if exists) is not associated with any active instance. If it finds a stale snapshot, it deletes it, effectively optimizing storage costs.

================Congratulation for Realtime Project Completeion=====================
