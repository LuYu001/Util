# autobuild.py

Forked from [carya/Util](https://github.com/carya/Util)
- 添加了描述字段
- 重写了获取IPA目录的方法
- 指定使用Python版本

iOS 自动化打包脚本，并上传*ipa*文件至蒲公英。
## 参数说明:

```
Usage: autobuild.py [options]

Options:
  -h, --help            show this help message and exit
  -w name.xcworkspace, --workspace=name.xcworkspace
                        Build the workspace name.xcworkspace.
  -p name.xcodeproj, --project=name.xcodeproj
                        Build the project name.xcodeproj.
  -s schemename, --scheme=schemename
                        Build the scheme specified by schemename. Required if
                        building a workspace.
  -m description, --desc=description
                        Pgyer update description.
```

## 使用方式:
```
./autobuild.py -p youproject.xcodeproj -s schemename -m 'description'
或者
./autobuild.py -w youproject.xcworkspace -s schemename -m 'description'
```

示例:
```
./autobuild.py -w ../abc.xcworkspace -s abc -m '添加了一个大功能'
```

### 脚本中有几个全局变量，根据自己项目设置进行修改其值, 包括:

```
CONFIGURATION = "Release"
EXPORT_OPTIONS_PLIST = "exportOptions.plist"
#会在文稿创建输出ipa文件的目录
EXPORT_MAIN_DIRECTORY = "~/Documents/"
```

*CONFIGURATION*：可在项目工程文件所在目录执行`xcodebuild -list`查看所有可选取值。

*EXPORT_OPTIONS_PLIST*：导出*ipa*文件时的配置参数，该参数值是你的配置参数文件名，请在*autobuild.py*文件所在目录下创建*exportOptions.plist*文件，配置参数可使用`xcodebuild --help`查看所有可选取值。

*EXPORT_MAIN_DIRECTORY*：默认情况下会在 `~/Documents` 创建*ipa*文件导出的文件夹，文件夹命名如:`~/Documents/{scheme}{2016-12-28_08-08-10}*`

### 上传*ipa*文件至蒲公英的配置，你需要设置的是:*USER_KEY*, *API_KEY*, *PYGER_PASSWORD*。

```
# configuration for pgyer
PGYER_UPLOAD_URL = "https://qiniu-storage.pgyer.com/apiv1/app/upload"
DOWNLOAD_BASE_URL = "https://www.pgyer.com"
USER_KEY = "15d6xxxxxxxxxxxxxxxxxx"
API_KEY = "efxxxxxxxxxxxxxxxxxxxx"
#设置从蒲公英下载应用时的密码,若无留空
```


