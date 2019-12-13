# vbx-server

## 杂记
好友关系可以用redis的有序集合存储
备注可以和doveid一起写到字符串里，星标可以存在score里

mysql用friend表存uid和fid

redis和mysql都存好友关系，Redis的Set数据类型提供良好的交并差集的计算支持，可以针对这些好友信息数据进行共同好友、可能认识的人等相关的操作

用户表用mysql存储

用户的对话记录在本地，聊天记录后端就不存了

## 日志

2019-12-03：实现了注册功能，整体逻辑我感觉很不行，但是已经折腾了很多遍了都不太满意，现在的大概流程是，main里接一个链接，判断请求类别，注册类别的信息就交给数据口接口类的注册方法，注册方法实例化注册类，去和数据库交互

2019-12-04：把整体代码逻辑重写了，这回感觉像点样子了，就是一个处理器的多态实现，不像之前一样无病呻吟，又加了一个responsepackage类，写的过程中发现错误处理不是很会弄，还不知道要不要输出个错误日志出来

2019-12-09：今天把每个有可能遇到错误的地方，都把错误输出到了错误日志中，但是不太明白这个错误处理里面还应该写些什么，还有就是我那个handle方法里有可能出现的错误太多了，没办法在最后统一返回一个err，有可能会被覆盖，然后就每遇到err就直接return，总觉得不是很对，准备注册里再判断一下是否重名，然后其他的错误直接归类于服务器错误好了

2019-12-10：登录注册完成了，不知道为什么写的连接池不能关闭，可能是把整个池子都关了吧，不知道具体到每个连接着怎么关闭

2019-12-13：登录的时候服务器把用户的信息和他好友的信息都返回过去了，现在不会的是怎么在注册的时候把头像传到服务器上，然后用户每次登录的时候判断本地有没有这个用户的信息，如果没有的话服务器就把body填上，有的话就不返回....还没写，好麻烦啊....