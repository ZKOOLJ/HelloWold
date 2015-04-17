 因为公司的需求,最近需要研究cas的这个框架,在网上找了很多资料,自己也算有些体会.在这里记录下,方便以后再其他地方用到同样的东西,有参考的资料

一  cas4.0服务端的搭建

    CAS服务器端下载地址:http://downloads.jasig.org/cas/ 目前最新的版本的cas4.0.本人目前用的也是cas4.0

    1.下载好cas4.0以后,直接解压.然后复制根目录下的pom文件和cas-server-webapp的文件到单独的文件目录下.然后打开pom文件找到modules删除其他不用的module模块,只保留cas-server-webapp模块即可.因为项目采用的maven构建的,而且eclipse的m2e插件目前还没有支持到execution,所以我们还需要在pom文件中加入如下的代码

<plugin>
         <groupId>org.eclipse.m2e</groupId>
         <artifactId>lifecycle-mapping</artifactId>
         <version>1.0.0</version>
         <configuration>
          <lifecycleMappingMetadata>
           <pluginExecutions>
            <pluginExecution>
             <pluginExecutionFilter>
              <groupId>
               com.mycila.maven-license-plugin
              </groupId>
              <artifactId>
               maven-license-plugin
              </artifactId>
              <versionRange>[1.9.0,)</versionRange>
              <goals>
               <goal>check</goal>
              </goals>
             </pluginExecutionFilter>
             <action>
              <ignore></ignore>
             </action>
            </pluginExecution>
            <pluginExecution>
             <pluginExecutionFilter>
              <groupId>
               org.apache.maven.plugins
              </groupId>
              <artifactId>
               maven-checkstyle-plugin
              </artifactId>
              <versionRange>[2.10,)</versionRange>
              <goals>
               <goal>checkstyle</goal>
              </goals>
             </pluginExecutionFilter>
             <action>
              <ignore></ignore>
             </action>
            </pluginExecution>
            <pluginExecution>
             <pluginExecutionFilter>
              <groupId>org.codehaus.mojo</groupId>
              <artifactId>
               aspectj-maven-plugin
              </artifactId>
              <versionRange>[1.4,)</versionRange>
              <goals>
               <goal>compile</goal>
              </goals>
             </pluginExecutionFilter>
             <action>
              <ignore></ignore>
             </action>
            </pluginExecution>
           </pluginExecutions>
          </lifecycleMappingMetadata>
         </configuration>
        </plugin>

最后用IDE导入项目(注:此导入时用maven类型导入),在发布项目到tomcat中,启动成功以后输入http://127.0.0.1:8080/cas/login就可以看到如下页面:



如此就代表服务端部署成功.(注:在页面上有红字的提醒,需要你删掉src\main\webapp\WEB-INF\view\jsp\default\ui\ casLoginView.jsp一行代码如图下,这样页面上面的提示就没有了)如下图:



2.部署成功以后就开始登录,在登录以前我们需要查看下deployerConfigContext.xml配置文件中的配置的用户名和密码,如图下:




在登录界面输入对应的用户名和密码,就可以登陆成功如下图:




以上就是一个完全的cas4.0的服务端框架的基本搭建.下一节将搭建cas客户端的使用和搭建
