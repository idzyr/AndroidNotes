# 为应用签名



## 了解密钥、证书和密钥库

> 以下内容因引用自https://developer.android.google.cn/studio/publish/app-signing 略有改动。

### 密钥

用于为用户设备上安装的 APK 签名的密钥称为**应用签名密钥**。作为 Android 安全更新模型的一部分，应用签名密钥在应用的整个生命周期内保持不变。应用签名密钥属于私钥，因此必须保密。不过，您可以与他人共享使用应用签名密钥生成的证书。

### 证书

**公钥证书**（`.der` 或 `.pem` 文件，也称为数字证书或身份证书）包含公钥或私钥对中的公钥，以及可以标识持有对应私钥的所有者的一些其他元数据（例如名称和位置）。通过密钥就可以生成证书。

在为您的应用签名时，签名工具会将该证书附加到应用。该证书会将 APK 或 App Bundle 与您和您对应的私钥相关联。这有助于 Android 确保您应用日后的所有更新都真实可靠，并且来自原始作者。

**证书指纹**是证书独一无二的简短表示形式，通常 API 提供商会要求同时提供证书指纹和软件包名称，以注册使用其服务的应用。您可以在 Play 管理中心的“应用签名”页面上找到上传证书和应用签名证书的 MD5、SHA-1 和 SHA-256 指纹。您还可以从同一页面下载原始证书 (`.der`) 来计算其他指纹。

### 密钥库

Java 密钥库（`.jks` 或 `.keystore`）：一个二进制文件，用作证书和私钥的存储区。**Play Encrypt Private Key (PEPK) 工具**：使用此工具可从 Java 密钥库中导出私钥。



## 生成密钥库

### AS生成

1. 在菜单栏中，依次点击 **Build > Generate Signed Bundle/APK**。

2. 在 **Generate Signed Bundle or APK** 对话框中，选择 **Android App Bundle** 或 **APK**，然后点击 **Next**。

3. 在 **Key store path** 字段下，点击 **Create new**。

   ![image-20210306162122647](signature-images/image-20210306162122647.png)

4. 在 **New Key Store** 窗口中，为您的密钥库和密钥提供以下信息。

   ![image-20210306193310808](signature-images/image-20210306193310808.png)

<img src="signature-images/keystore-wizard_2x.png" alt="img" style="zoom:50%;" />

5. 填写完表单后，请点击 **OK**。有可能会出现以下错误。有关如何解决此问题请看下面 [迁移密钥到PKCS12](#迁移密钥到PKCS12)

   ![image-20210306202107114](signature-images/image-20210306202107114.png)

### KeyTool

#### keytool指令

以下列出在下面章节中要使用到的部分命令。

```bash
# 命令:
 -certreq            生成证书请求
 -changealias        更改条目的别名
 -delete             删除条目
 -exportcert         导出证书
 -genkeypair         生成密钥对 -genkey #简写
 -genseckey          生成密钥
 -gencert            根据证书请求生成证书
 -importcert         导入证书或证书链
 -importpass         导入口令
 -importkeystore     从其他密钥库导入一个或所有条目
 -keypasswd          更改条目的密钥口令
 -list               列出密钥库中的条目
 -printcert          打印证书内容
 -printcertreq       打印证书请求的内容
 -printcrl           打印 CRL 文件的内容
 -storepasswd        更改密钥库的存储口令
```

- `-genkey` 生成密钥对

  ```bash
  # 选项:
   -alias <alias>                  要处理的条目的别名
   -keyalg <keyalg>                密钥算法名称
   -keysize <keysize>              密钥位大小
   -sigalg <sigalg>                签名算法名称
   -destalias <destalias>          目标别名
   -dname <dname>                  唯一判别名
   -startdate <startdate>          证书有效期开始日期/时间
   -ext <value>                    X.509 扩展
   -validity <valDays>             有效天数
   -keypass <arg>                  密钥口令
   -keystore <keystore>            密钥库名称
   -storepass <arg>                密钥库口令
   -storetype <storetype>          密钥库类型
   -providername <providername>    提供方名称
   -providerclass <providerclass>  提供方类名
   -providerarg <arg>              提供方参数
   -providerpath <pathlist>        提供方类路径
   -v                              详细输出
   -protected                      通过受保护的机制的口令
  ```

- `-importkeystore`  从其他密钥库导入一个或所有条目

  ```bash
  # 选项:
   -srckeystore <srckeystore>            源密钥库名称
   -destkeystore <destkeystore>          目标密钥库名称
   -srcstoretype <srcstoretype>          源密钥库类型
   -deststoretype <deststoretype>        目标密钥库类型
   -srcstorepass <arg>                   源密钥库口令
   -deststorepass <arg>                  目标密钥库口令
   -srcprotected                         受保护的源密钥库口令
   -srcprovidername <srcprovidername>    源密钥库提供方名称
   -destprovidername <destprovidername>  目标密钥库提供方名称
   -srcalias <srcalias>                  源别名
   -destalias <destalias>                目标别名
   -srckeypass <arg>                     源密钥口令
   -destkeypass <arg>                    目标密钥口令
   -noprompt                             不提示
   -providerclass <providerclass>        提供方类名
   -providerarg <arg>                    提供方参数
   -providerpath <pathlist>              提供方类路径
   -v                                    详细输出
  ```



#### 命令行生成密钥

输入以下命令

```bash
# 格式
keytool -genkey -alias 密钥别名 -keypass 密钥密码 -keyalg 密钥算法名称 -keysize 密钥位大小 -validity 有效天数 -keystore 密钥库名称（包含路径.keystore） -storepass 密钥库密码

# 示例
keytool -genkey -alias demo -keypass 123123 -keyalg RSA -keysize 2048 -validity 366 -keystore ./deom.keystore -storepass 321321
```

![image-20210306211441320](signature-images/image-20210306211441320.png)

 ![image-20210306211548822](signature-images/image-20210306211548822.png)

以上警告将在下一节中介绍如何处理。

#### 迁移密钥到PKCS12

> 解决提示；JKS 密钥库使用专用格式。建议使用 "keytool -importkeystore -srckeystore E:\xxxxxx- pkcs12" 迁移到行业标准格式PKCS12

![image-20210308205620237](signature-images/image-20210308205620237.png)

如果你按照keytool中给出的指令（上图中引号内的指令建议复制到其它文本编辑器确认无回车符后执行）执行后提示如下请按照以下命令进行尝试。

![image-20210308210346952](signature-images/image-20210308210346952.png)



```bash
# 格式；
keytool -importkeystore -srckeystore 源密钥库名称 -destkeystore 目标密钥库名称 -deststorepass  目标密钥库密码 -deststoretype 目标密钥库类型

# 示例
keytool -importkeystore -srckeystore ./deom.keystore -destkeystore ./deom.keystore -deststorepass 321321 -deststoretype pkcs12
```



![image-20210306222259890](signature-images/image-20210306222259890.png)

![image-20210306222358158](signature-images/image-20210306222358158.png)

可以看到之前密钥库已经被天机`.old`作为备份，要使用就用没有`old`后缀的密钥库文件。

> **注意；**
>
> 当使用迁移后的密钥进行打包时会报`Given final block not properly padded. Such issues can arise if a bad key is used during decryption.` 出现这种问题是我们输入的密钥密码错误导致的，实际这里的密码和密钥库密码是一样的（也就是上面我在命令中设置的321321），而非我们迁移密钥库前的密钥密码。我也是后来才知道至于为啥出现这种问题这里不深究了。下面我会介绍如何解决此问题。

如果你在执行完上述命令后出现以下错误。请尝试以下指令。

![image-20210308212920199](signature-images/image-20210308212920199.png)

```bash
# 格式
keytool -importkeystore -srckeystore 源密钥库 -destkeystore 目标密钥库 -deststorepass 目标密钥库密码 -destkeypass 目标密钥库密钥密码 -deststoretype 目标密钥库类型

# 示例
keytool -importkeystore -srckeystore .\xx.jks -destkeystore .\xx.jks -deststorepass xx -destkeypass xx -deststoretype pkcs12
```

![image-20210308213619203](signature-images/image-20210308213619203.png)

> **注意；**
>
> 这里和上面一样在使用迁移后的密钥库时，密钥库密码和密钥库密钥密码一致。

**解决密钥库密钥和密钥相同问题；**

详细参考；[直接生成PKCS12](#直接生成PKCS12)步骤二

#### 直接生成PKCS12

1. 执行下面命令

   ```bash
   # 格式
   keytool -genkey -v -alias 密钥别名 -keyalg 密钥算法名称 -storetype 密钥库类型 -keystore 密钥库名称 -storepass 密钥库密码 -keypass 密钥密码 -validity 密钥库有效期
   # 示例
   keytool -genkey -v -alias demo -keyalg RSA -storetype PKCS12 -keystore ./demo.keystore -storepass 123123 -keypass 321321 -validity 3600
   ```

   ![image-20210307152259386](signature-images/image-20210307152259386.png)

2. 此时生成的证书确实是pkcs12，但alias的口令（密码）与密钥库的口令一样，如果这样能满足你的需求，那就不用往下看了。但一般我们不希望别名和秘钥库的口令是一样的，所以接下来我们用命令修改刚才创建的别名口令即可。

   ```bash
   # 格式
   keytool -keypasswd -alias 密钥别名 -keystore 密钥库。
   # 示例；
   keytool -keypasswd -alias demo -keystore ./demo.keystore.jks
   ```

   ![image-20210308200126949](signature-images/image-20210308200126949.png)

#### 查看密钥库详情

```bash
# 格式
keytool -list -v -keystore 密钥库
# 示例
keytool -list -v -keystore ./deom.keystore
```

![image-20210308214219142](signature-images/image-20210308214219142.png)

## 使用密钥为应用签名

### Android App Bundle 

Android App Bundle 是一种发布格式，其中包含您应用的所有经过编译的代码和资源，它会将 APK 生成及签名交由 Google Play 来完成。

Google Play 会使用您的 App Bundle 针对每种设备配置生成并提供经过优化的 APK，因此只会下载特定设备所需的代码和资源来运行您的应用。您不必再构建、签署和管理多个 APK 来优化对不同设备的支持，而用户也可以获得更小且更优化的下载文件包。

### APK

1. 如果您目前没有打开 **Generate Signed Bundle or APK** 对话框，请依次点击 **Build > Generate Signed Bundle/APK**。

2. 在 **Generate Signed Bundle or APK** 对话框中，选择  **APK**，然后点击 **Next**。

   ![image-20210306193817343](signature-images/image-20210306193817343.png)

3. 从下拉菜单中选择一个模块。

4. 指定密钥库的路径、密钥的别名，然后输入二者的密码。key alias选择存储在密钥库里的别名。如果您尚未准备好上传密钥库和密钥，请先[生成上传密钥和密钥库](#生成密钥库)，然后返回完成此步骤。

   ![image-20210306194324045](signature-images/image-20210306194324045.png)

![image-20210306194744537](signature-images/image-20210306194744537.png)

![image-20210306225440363](signature-images/image-20210306225440363.png)

5. 点击 **Next**。

6. 为签名的应用选择一个目标文件夹，选择构建类型，然后选择产品变种（如果适用）。

   > **注意；**
   >
   > debug默认不使用系统签名，而且对一些文件图片的格式校验比较松，还有就是一些string.xml文件或其他xml文件命名校验不是很严格，不必进行强制编译

   ![image-20210306195332141](signature-images/image-20210306195332141.png)

- **V1；**就是传统的签名方式，
- **V2；**则是Android7.0之后引入的。
- **其区别是；**V1是通过ZIP条目进行验证，这样APK 签署后可进行许多修改；而V2验证压缩文件的所有字节，而不是单个 ZIP 条目，这样在签名后无法再更改。V2的好处很明显，更安全且验证更迅速。所以，推荐在生成apk时，签名方式选择V1+V2。当然，仅仅选择V1也是可以的。**如果仅选择V2呢**，这样生成的apk在Android7.0及之后的版本上没有问题，不过会导致7.0以下的版本无法安装，所以要避免这种方式。

debug方式；

![image-20210306225019047](signature-images/image-20210306225019047.png)



release方式；

![image-20210306225746806](signature-images/image-20210306225746806.png)



## 自动签名打包

首先在Android studio 右击项目选择 Open module settings

![img](signature-images/20200512142219768.jpg)

填写完成点击应用、OK后会在 Module：app （build.gradle）生成代码：

![img](signature-images/20200512142834837.jpg)

 

好了到这里就基本完成了。