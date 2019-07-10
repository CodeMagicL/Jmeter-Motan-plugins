# Jmeter-Motan-plugins
Jmeter Test MotanRpc plugins
本文主要介绍Jmeter Motan协议的使用方法
引入插件包
将插件包jmeter-plugins-motan.jar拷贝到JmeterHome\lib\ext目录下

创建MotanSample
1.打开Jmeterm并且创建一个线程组



2.在Jmeter测试计划底部引入被测Motan接口服务jar包



3.创建MotanSample 创建线程组->add->sample->Motan sample



4.填写测试Motan接口信息



MotanSample-界面参数解析
  * name            - sample名称
  * motan xml path  - motanService服务的xml配置文件路径
  * interface       - 被测服务名称需要与xml文件中的motan:referer id一致
  * method          - 被测方法名称
  * args            - 被测方法的参数，paramType必须填写，参数基础类型名称 或 包装类完全名（含包名）、paramValue为参数值

常规参数对照表
方法入参类型	paramType	paramValue
int	int	1
int[]	int[]	[1,2]
double	double	1.2
double[]	double[]	[1.0,1.2]
short	short	1
short[]	short[]	1
float	float	1.3
float[]	float[]	[3.2,3.1]
long	long	1
long[]	long[]	[1,2]
byte	byte	字节内容
byte[]	byte[]	字节内容
boolean	boolean	true | false
boolean[]	boolean[]	[true,false]
char	char	a
char[]	char[]	[a,b]
java.lang.String	java.lang.String |String |string	too
java.lang.String[]	java.lang.String[] | String[] | string[]	["too-1","too2"]
java.lang.Integer	java.lang.Integer | Integer | integer	1
java.lang.Integer[]	java.lang.Integer[] | Integer[] | integer[]	[1,2,3]
java.lang.Double	java.lang.Double | Double	1.2
java.lang.Double[]	java.lang.Double[] | Double[]	[1.2,1.3]
java.lang.Short	java.lang.Short | Short	1
java.lang.Short[]	java.lang.Short[] | Short[]	[1,2]
java.lang.Long	java.lang.Long | Long	1
java.lang.Long[]	java.lang.Long[] | Long[]	[1,2]
java.lang.Float	java.lang.Float | Float	1.2
java.lang.Float[]	java.lang.Float[] | Float[]	[1.1,1.2]
java.lang.Byte	java.lang.Byte | Byte	字节内容
java.lang.Byte[]	java.lang.Byte[] | Byte[]	字节内容
java.lang.Boolean	java.lang.Boolean | Boolean	true | false
java.lang.Boolean[]	java.lang.Boolean[] | Boolean[]	[true ,false]
复杂参数的使用
/**
普通javaBean
***/
package io.hst;
import java.io.Serializable;
public class ExampleBean  implements Serializable{
    private static final long serialVersionUID = -181200840099007640L;
    private String name;
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
}  

  /****
  泛型javaBean
  *****/
package io.hst;
import java.io.Serializable;
public class ExampleVo<T> implements Serializable {
    private static final long serialVersionUID = 4758500884970862250L;
    private T mValue;
 
    public T getmValue() {
        return mValue;
    }
 
    public void setmValue(T mValue) {
        this.mValue = mValue;
    }
}

方法入参类型	paramType	paramValue
io.hst.ExampleBean	io.hst.ExampleBean	{"name":"123456"}
io.hst.ExampleBean[]	io.hst.ExampleBean[]	[{"name":"123456"}]
io.hst.ExampleVo<ExampleBean>	io.hst.ExampleVo	{"mValue": {"class": "io.hst.ExampleBean","name": "123456"}
java.util.List<ExampleBean>	java.util.List	[{"class": "io.hst.ExampleBean","name":"123456"}]
java.util.List<ExampleBean>[]	java.util.List[]	[[{"class": "io.hst.ExampleBean","name":"123456"}]]
java.util.Map<String, ExampleBean>	java.util.Map	{"key":{"class": "io.hst.ExampleBean","name":"123456"}}
java.util.Map<String, ExampleBean>[]	java.util.Map[]	[{"key":{"class": "io.hst.ExampleBean","name":"123456"}}]
