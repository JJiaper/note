方法一： 添加 context 标签

```
 <context:property-placeholder location="classpath:application.properties"/>


```

![](http://hiper.top/upload/2019/3/image-155609352527220190424081204318.png)

方法二：

```
  
    <bean  
       >  
        <property  />  
    </bean> 


```

方法三：

```
<bean
  >
   <property >
      <list>
         <value>config/connects.properties</value>
         <value>config/zookeeper.properties</value>
         <value>config/other.properties</value>
         
         
         
      </list>
   </property>
</bean>


```

使用的时候 ${这个位置填写配置文件的键} ![](http://hiper.top/upload/2019/3/image-155609357101620190424081249294.png)

本文由 [彭效佳](http://hiper.top/) 创作，采用 [知识共享署名 4.0](https://creativecommons.org/licenses/by/4.0/) 国际许可协议进行许可  
本站文章除注明转载 / 出处外，均为本站原创或翻译，转载前请务必署名  
最后编辑时间为: 一月 10,2020