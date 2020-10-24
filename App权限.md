# App权限

android6.0 也就是api lev 为23，

- android6.0+的权限叫做run-time permission
- android6.0以下的权限叫做install-time permission

所有用到的权限都要在`AndroidManifest`中申请。

## 基本用法

> 以下大部分方法来自**ActivityCompat**类提供的方法。

### 权限检查

- `checkSelfPermission(String);` 权限检测方法
  - 参数
    - 权限常量名
  - 返回值 int 
    - 有权限返回PackageManager.PERMISSION_GRANTED 代表值0
    -  没有权限返回 PackageManager.PERMISSION_DENIED 代表值-1

```java
btnCheckSelfPermission.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                //检测权限
                int readPermissian = checkSelfPermission(Manifest.permission.READ_EXTERNAL_STORAGE); //读取存储卡权限
                int writePermissian = checkSelfPermission(Manifest.permission.WRITE_EXTERNAL_STORAGE);//写入存储卡
                //处理结果
                if (readPermissian != PackageManager.PERMISSION_GRANTED || writePermissian != PackageManager.PERMISSION_GRANTED) {
                    Log.d(TAG, "onClick: 当前无权限");
                }else {
                    Log.d(TAG, "onClick: 当前已经有权限了");
                }
            }
        });
```



### 请求权限

- `requestPermissions(String[],int)`  请求权限
  - 参数
    - String[] permissions 权限字符串组
    - int requestCode 请求码

```java
        btnRequestPermission.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                int storageGroupPermassion = checkSelfPermission(Manifest.permission_group.STORAGE);
                if (storageGroupPermassion != PackageManager.PERMISSION_GRANTED) {
                    Log.d(TAG, "onClick: 当前无权限");
/*--------------------------------------*/
                    //请求权限
                    requestPermissions(new String[]{Manifest.permission_group.STORAGE}, PERMISSION_REQUEST_CODE);

                }
            }
        });

```

- `requestPermissions(Activity，String [],int)` 请求权限重载
  - Activity activity  目标活动
  - String[] permissions 权限字符串组
  - int requestCode 请求码

**处理请求结果；**

重写`onRequestPermissionsResult` 方法

- `onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)`
  - 形参说明；
    - int requestCode 请求码，发起权限请求时设置的那个请求码。
    - String[] permissions 发起请求的权限数组
    - int[] grantResults 每项权限授予结果。
      - 同意 值为PackageManager.PERMISSION_GRANTED 代表值0
      - 拒绝 值为 PackageManager.PERMISSION_DENIED 代表值-1

```java
    //重写权限请求结果回调
    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
        //校验请求码
        if (requestCode == PERMISSION_REQUEST_CODE) {
            //判断请求结果
            if (grantResults.length >= 1 && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                Log.d(TAG, "onRequestPermissionsResult: 有权限了可以执行其它操作了");
                return;
            } else {
                Log.d(TAG, "onRequestPermissionsResult: 用户没有同意权限");
                //如果不给权限就不让用哈哈
                finish();
            }
        }
    }
```

**显示请求许可理由；**

如果用户拒绝了权限请求，提示介绍要必要权限的原因，用户同意后再次申请权限。

- `ActivityCompat.shouldShowRequestPermissionRationale()` 是否可以显示请求许可UI界面，如果可以我们显示请求许可理由，否则就引导用户到app设置手动开启权限。 

  - 参数
    - Activity activity   目标活动
    - String permission 您的应用要请求的权限
  - 返回
    - 可以显示 返回true
    - 不可以显示false

  **说明；**

  1. 第一次请求权限返回false
  2. 第一次请求权限被拒绝并且为勾选不在询问返回 true
  3. 某权限被允许后返回false
  4. 禁止某权限并勾选不在询问返回false

  **问题；**

  在国产手机中此`ActivityCompat.shouldShowRequestPermissionRationale()`方法一直返回false。如小米手机，这种问题建议直接跳转到应用详情界面让用户手动开启。

```java
    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
        //校验请求码
        if (requestCode == PERMISSION_REQUEST_CODE) {
            //判断请求结果
            if (grantResults.length >= 1 && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                Log.d(TAG, "onRequestPermissionsResult: 有权限了可以执行其它操作了");
            } else {
                Log.d(TAG, "onRequestPermissionsResult: 用户没有同意权限");



                /*--------------解释权限作用，再次申请权限部分国产系统一之返回false------------------------*/

                if (ActivityCompat.shouldShowRequestPermissionRationale(this, Manifest.permission.WRITE_EXTERNAL_STORAGE)) {
                    //展示权限请求理由
                    Log.d(TAG, "onRequestPermissionsResult: 解释权限用途");
                    //以对话框形式展示
                    AlertDialog.Builder dialog = new AlertDialog.Builder(this);
                    dialog.setTitle("权限说明");
                    dialog.setMessage("请给予必要权限否则APP无法运行");
                    dialog.setCancelable(false); //设置是否可以取消
                    //注册用户点击正确按钮事件。
                    dialog.setPositiveButton("好的", new DialogInterface.OnClickListener() {
                        @Override
                        public void onClick(DialogInterface dialogInterface, int i) {
                            //再次请求权限
                            ActivityCompat.requestPermissions(Authority.this, new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE}, PERMISSION_REQUEST_CODE);
                        }
                    });
                    dialog.show();     //展示对话框。
                } else {
                    /*--------用户依然拒绝了我们的请求----------------*/
                    //引导用户到app设置中开启权限
                    Log.d(TAG, "onRequestPermissionsResult: 跳转到手动开启权限");
                    /*------------再次解释权限重要性并引导用户手动开启权限--------------------------*/
                    AlertDialog.Builder dialog = new AlertDialog.Builder(this);
                    dialog.setTitle("提示");
                    dialog.setMessage("请在应用应用详情->权限管理->打开读写手机存储权限\r\n避免影响正常使用");
                    dialog.setPositiveButton("确认", new DialogInterface.OnClickListener() {
                        @Override
                        public void onClick(DialogInterface dialogInterface, int i) {
                            Intent intent = new Intent(Settings.ACTION_APPLICATION_DETAILS_SETTINGS);
                            Uri uri = Uri.fromParts("package", getPackageName(), null);
                            intent.setData(uri);
                            startActivity(intent);  //跳转到手动激活页面。
                        }
                    });

                    dialog.setNegativeButton("取消", new DialogInterface.OnClickListener() {
                        @Override
                        public void onClick(DialogInterface dialogInterface, int i) {
                            Log.d(TAG, "onClick: 拒绝了权限申请");
                        }
                    });
                    dialog.show();  //显示对话框


                }

            }
        }
    }
```

效果展示；

![permission_demo](App%E6%9D%83%E9%99%90-images/permission_demo.gif)

## 第三方库

### XXPermissions

> GitHub；https://github.com/getActivity/XXPermissions

slogan；

一行代码搞定动态权限获取



**集成**

```gr
dependencies {
    implementation 'com.hjq:xxpermissions:8.8'
}
```



#### 权限检测

```java
        btnCheckSelfPermissionLib.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
               if(XXPermissions.hasPermission(Authority.this,new String[]{Manifest.permission_group.STORAGE})){
                    Log.d(TAG, "onClick: 权限已经授予");
               }else {
                   Log.d(TAG, "onClick: 权限为获取");
               }
            }
        });
```



#### 权限申请

```java
btnRequestPermissionLib.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {

                XXPermissions.with(Authority.this)
                        // 申请安装包权限
                        //.permission(Permission.REQUEST_INSTALL_PACKAGES)
                        // 申请悬浮窗权限
                        //.permission(Permission.SYSTEM_ALERT_WINDOW)
                        // 申请通知栏权限
                        //.permission(Permission.NOTIFICATION_SERVICE)
                        // 申请系统设置权限
                        //.permission(Permission.WRITE_SETTINGS)
                        // 申请单个权限
                        //.permission(Permission.RECORD_AUDIO)
                        .permission(Permission.Group.STORAGE) //要申请的权限
                        .request(new OnPermission() {   //开始申请权限
                            @Override
                            public void hasPermission(List<String> granted, boolean all) {
                                //又权限回调
                                if (all){
                                    Log.d(TAG, "hasPermission: 所有权限以都给予");
                                }else {
                                    Log.d(TAG, "hasPermission: 部分权限为给予");
                                }

                            }

                            @Override
                            public void noPermission(List<String> denied, boolean never) {
                                //无权限回调
                                if (never){
                                    // 被永久拒绝的权限处理。

                                    //TODO 展示请求权限原因，引导用户手动开启权限。
                                    // 如果是被永久拒绝就跳转到应用权限系统设置页面
                                    XXPermissions.startPermissionActivity(Authority.this, denied);
                                    Log.d(TAG, "noPermission: 进入权限管理界面让用户手动授权");
                                }else {
                                    Log.d(TAG, "noPermission: 权限申请失败可能被拒绝");
                                }
                            }
                        });
            }
        });
```



