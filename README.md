Jenkins file we need to keep on GIT along with ansible playbook and inventory.
This Tomcat job is used to restart Tomcat for versions 7 and 8. Additionally, it will display the current Tomcat status along with system metrics.

Job Details:
  Job Name: TomcatRestart
  Trigger: Manually
  Environment: Metrology
Steps:
  Stop Tomcat txn instances for versions 7 and 8
  Wait for a few seconds
  Start Tomcat txn instances for versions 7 and 8
  It can be use to restart web service if user wants
  Another task of this jenkins pipelines to clear only logs
Status and Metrics Display:
  The job will display the following information:
    Current status of Tomcat txn instances
    System metrics such as CPU usage, memory usage, and disk space
