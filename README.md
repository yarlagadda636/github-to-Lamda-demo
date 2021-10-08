# github-to-lambda-demo

This repo contains the source code for my YouTube video (https://www.youtube.com/watch?v=AmHZxULclLQ) where I talk about how to automatically update aws lambda function code using CodeBuild (i.e., CI/CD of AWS Lambda Deployment).

=======================================================================================================================
                   CI/CD from GitHub to AWS Lambda - https://github.com/felixyu9/github-to-lambda-demo
=======================================================================================================================
Step 1:-
       Create a Lamda Function
       Function Name 		github-to-Lamda-demo
       Runtime       		phython 3.8
Step 2:-
       Create a GitHub Repository
       Repository Name		github-to-lamda-demo
       Options                  public
                                Add a Readme file
 				Add .gitignore  phython
       Create Repository        Yes
Step 3:-
       git bash                 local laptop
       Open                     local laptop cd to folder
       Clone the Repository     git clone https://github.com/felixyu9/github-to-lambda-demo.git
       Navigate                 cd github-to-lamda-demo
       vscode                   code . or open vscode and go to folder
Step 4:- 
       AWS console              Go to lamda function,find out the handler info
                                Lamda-function.lamda-handler
       vscode                   create a file lamda-functon.py (like in handler info) 
       vscode                   in lamda-function.py file write a handler
       vscode                   create 2nd file requirements.txt
       vscode                   create 3rd file buildspec.yml 
Step 5:-
       git bash                 git add .
                                git commit -m 'added lambda code'
                                git push https://github.com/xxxx/xxxx
Step 6:- 
      CodeBuild                 Project Name: github-to-lambda
                                Source provider: GitHub
                                Connect to GitHub : Authenticate
                                Repository in my GitHub account
                                GitHub repository   https://github.com/felixyu9/github-to-lambda-demo.git
                                Source version - optional Info   : main
                                Primary source webhook events : Rebuild every time a code change is pushed to this repository
                                Event type : PUSH
                                Operating system : Ubuntu
                                Runtime(s) :  standard
                                Image : aws/codebuild/standard:5.0
                                Logs:  CloudWatch  uncheck CloudWatch logs - optional
                                Create build project.
Step 7:-
     Permissions                Give CodeBuild project to update Lambda function.
     CodeBuild                  Go to BuildDetails Environment : Service role. Click on the link.
                                Click on policy.  Edit policy
                                 {
                                "Effect": "Allow",
                                "Action": [
                                    "lambda:AddPermission",
                                    "lambda:RemovePermission",
				    "lambda:CreateAlias",
                                    "lambda:UpdateAlias",
                                    "lambda:DeleteAlias",
                                    "lambda:UpdateFunctionCode",     
                                    "lambda:UpdateFunctionConfiguration",
				    "lambda:PutFunctionConcurrency",
	                            "lambda:DeleteFunctionConcurrency",
				    "lambda:PublishVersion"
                                 ],
                                "Resource": "arn:aws:lambda:us-east-1:your-aws-account-number:function:your-lambda-function"
                              },
                              Replace Resource arn with lamda function arn
                              click on Review Policy and Save changes.
Step 8:-
      Testing                 update print('Done x1') with print('Done x2')  
                              git push
                              From AWS Management Console.  Go to Lambda function. Test
                              Type testEvent {}  create
                              test, Details.  You can see the output with x2.

   

=======================================================================================================================




                             
        

 