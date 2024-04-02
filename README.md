# AWS_serial_console_checker
Deploy:
aws cloudformation create-stack --stack-name serialconsolechecker--capabilities CAPABILITY_NAMED_IAM --template-body file://cloudformation_template.yaml 

1. I enabled alarm, which is checking if SerialConsole was turned on globally(As i understood correctly the documentation it must be done per region). Alarm starts 2 lambdas. Adding sns or different solution to alert is not huge deal so i was not adding this.
2. Unfortunately if something went south and somebody turned on Serial Console it would be worth to check who have possibilty to do so... That's the job of TrailPermissionCheckerLambda. In my opinion it is not daily occurence so i left that information in lambda log stream, we could use EventBridghe or save it in s3 but idk if it's worth the resources.
3. Second lambda turns off serial console access.
4. After everything Alarm should turn itself to OK state. 
