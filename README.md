# RobotFramework-Jenkins-Pipeline-Support-Example
This Jenkinsfile creates a pipeline with support for the [Robotframework Jenkins Plugin](https://plugins.jenkins.io/robot).

This is a rough example to show how easily robotframework can be integrated into your Jenkins CI Environment even though it is not officially supported for pipelines. 

In this case the tests are run every 15 minutes and are executed on any available Jenkins slave under the 'slave-01' label.

### Common issues
On most Jenkins setups further steps will be required to view robotframework logs and reports  
as Jenkins by default disables js execution.  

A temporary workaround is to execute the following in the script console to lax the security requirements.
```GROOVY
System.setProperty("hudson.model.DirectoryBrowserSupport.CSP",
                   "sandbox allow-scripts allow-same-origin;
                   default-src 'none';
                   img-src 'self' data: ;
                   style-src 'self' 'unsafe-inline' data: ;
                   script-src 'self' 'unsafe-inline' 'unsafe-eval' ;\"");
```

