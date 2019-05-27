超链接目标地址

href后面是目标地址

template中可以用 **"{% url 'app_name:url_name' param %}"**

其中**app_name**和**url_name**都在url中配置



再配URL

url函数的名称参数

根urls，写在**include()**的第二个参数位置，**namespace='blog'**

应用在则写在**url()**的第三个参数位置，**name='article'**

主要取决于**是否使用include**引用了另一个url配置文件

