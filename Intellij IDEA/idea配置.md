# 1. 注释模板

## 1.1 类 注释

![image-20201102093648796](idea配置.assets/image-20201102093648796.png)  



```
/**
 * @Author:  Leo.xu
 * @Created: ${DATE} ${TIME}
 * @Description:
 */
```



## 1.2 方法注释

![image-20201102093825446](idea配置.assets/image-20201102093825446.png) 



![image-20201102093943114](idea配置.assets/image-20201102093943114.png) 



```
**
 *
 * @Auther: Leo.Xu
 * @Create: $date$ $time$
 * @Param:  $param$
 * @Return: $return$
 * @Description:
 */
```



![image-20201102094021834](idea配置.assets/image-20201102094021834.png) 



```
 groovyScript("  def result='';    def params=\"${_1}\".replaceAll('[\\\\[|\\\\]|\\\\s]', '').split(',').toList();     for(i = 0; i < params.size(); i++) {       if(i!=0)result+= ' * ';        result+=params[i] + ((i < (params.size() - 1)) ? '\\n' + '\\t' : '');     };      return result", methodParameters()) 
```



# 2. 关闭idea启动自动开启最近项目

![image-20201102115826455](idea配置.assets/image-20201102115826455.png) 