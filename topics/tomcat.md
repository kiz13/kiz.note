# Apache Tomcat

[config tomcat user to allow access to manager app](https://stackoverflow.com/questions/16671858/im-not-able-to-log-in-tomcat-manager-app) `$tomcat_home/conf/tomcat-users`

[manager gui access denied?](https://stackoverflow.com/questions/43232878/apache-tomcat-9-unable-to-access-manager-webapp) do this: in the `CATALINA_HOME/webapps/manager/META-INF/context.xml` file, comment out this Valve tag

  ```xml
  <Context antiResourceLocking="false" privileged="true" >
  <!--
  <Valve className="org.apache.catalina.valves.RemoteAddrValve" allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" />
  -->
  </Context>
  ```

or more properly, [add you machine's ip](https://stackoverflow.com/questions/38551166/403-access-denied-on-tomcat-8-manager-app-without-prompting-for-user-password) like `allow="xxx|xxx|your.freaking.ip.address"`

`java.nio.file.AccessDeniedException` how to allow permissions to a java app deployed on tomcat? [Permissions are always given to users, not to applications.](https://coderanch.com/t/731454/application-servers/Permission-permissions-java-app-deployed)
