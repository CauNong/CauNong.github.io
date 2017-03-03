---
title: UWP应用设置和文件设置：科普
date: 2017-03-03 10:13:24
tags: [设置,文件设置]
categories: UWP开发
---
**转自[姜子瑜](http://www.cnblogs.com/ldzhangyx/p/6235436.html)**  

### 数据有两个基本的分类，应用数据和用户数据。  

**用户数据**为由用户拥有的数据，如文档，音乐或电子邮件等，下面将大致的介绍一下应用数据的基本操作。  

**应用数据：**应用数据包含APP的状态信息（如运行时状态，用户设置等），包括设置和文件，应用数据在应用程序安装时有自己的存储区域，而在卸载时会清空  

**设置：**存储用户首选项和应用程序状态,可存储多种数据类型 <!--more-->  
>UInt8、Int16、UInt16、Int32、UInt32、Int64、UInt64、Single、Double  
>Boolean  
>Char16 和 String  
>DateTime 和 TimeSpan    
>GUID、Point、Size、Rect  

ApplicationDataCompositeValue：一组必须按原子方式序列化和反序列化的相关应用设置。使用复合设置可轻松处理相互依赖的设置的原子更新。系统会在并发访问和漫游时确保复合设置的完整性。复合设置针对少量数据进行了优化，如果将它们用于大型数据集，性能可能很差。  
文件：使用文件存储二进制文件，或自定义的序列化类型  
   

上面提到过应用数据包括设置和文件  

而应用数据根据存储的性质又分为三类：  

**本地数据**  
**漫游数据：**用户可轻松地在多个设备之间保持应用的应用数据同步  
**临时数据：**临时应用数据存储类似于缓存  
所以相应的就有本地设置和本地文件，漫游设置和漫游文件，临时设置和临时文件  

   

不同类型的设置和文件的API如下：

本地设置：ApplicationData.Current.LocalSettings  
本地文件：ApplicationData.Current.LocalFolder  
漫游设置：ApplicationData.Current.RoamingSettings  
漫游文件：ApplicationData.Current.RoamingFolder  
临时设置：ApplicationData.Current.TemporarySettings  
临时文件：ApplicationData.Current.TemporaryFolder  
   

### 设置的基本操作

设置是一个ApplicationDataContainer类型的对象，关于ApplicationDataContainer类的介绍请参照官方文档 ，这里只是介绍一些简单的操作。

   简单设置

    ApplicationDataContainer localSettings = ApplicationData.Current.LocalSettings;//获取本地设置，你也可以获取漫游设置和临时设置，后面的操作都一样
    localSettings.Values["theme"] = "Light";//在本地设置中添加一个设置项，类似字典赋值方式，theme是localSettings里面的key，而"Light"是值，可以设置的类型在上面已经列出
    localSettings.Values.Remove("theme");//删除设置项
    string theme = localSettings.Values["theme"] as string;//读取设置项

    ApplicationDataCompositeValue simpleSettings = new ApplicationDataCompositeValue();//创建简单设置的容器
    simpleSettings["theme"] = "Light";
    simpleSettings["FontFamily"] = "微软雅黑";
    localSettings.Values["SimpleSettings"] = simpleSettings;//将复合设置项添加到上面获取的本地设置中

    ApplicationDataCompositeValue advanceSettings = new ApplicationDataCompositeValue();//创建简单设置的容器
    advanceSettings["IsSync"] = false;
    localSettings.Values["AdvanceSettings"] = advanceSettings;

这样就可以实现设置项的复合操作，具体操作参照：[MSDN](https://msdn.microsoft.com/zh-cn/library/windows/apps/xaml/windows.storage.applicationdatacontainer.aspx)

### 文件的基本操作

与文件操作相关的两个基本的类是StorageFile和StorageFolder


    StorageFolder folder = ApplicationData.Current.LocalFolder;//获得本地文件夹
    StorageFile file = await folder.CreateFileAsync("first.txt", CreationCollisionOption.OpenIfExists);//创建文件
    await FileIO.WriteTextAsync(file, "文本的内容");//使用FileIO将字符串写入文件

    StorageFile fileOpen = folder.GetFileAsync("first.txt");
    string content = await FileIO.ReadTextAsync(fileOpen);//读取文本    

以上操作稍作修改就可应用于漫游数据和临时数据，漫游数据可以实现多设备间的数据同步，但是数据同步有一定的条件。临时数据类似于缓存，可用于保存一些缓存数据，如微博里的图片缓存等，系统维护时会自动删除，或者可以随时手动删除。

除了对数据的操作之外，你也可以对数据进行版本控制：使用Application.Version属性和ApplicationData.SetVersionAsyncthe new text here

