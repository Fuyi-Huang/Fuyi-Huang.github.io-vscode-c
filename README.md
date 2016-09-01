### 总体流程
1.下载安装vscode

2.安装cpptools

3.安装编译环境

4.修改vscode调试配置文件


### 下载安装vscode
[http://code.visualstudio.com](http://code.visualstudio.com)

### 安装cpptools
打开你的vscode，按ctrl + e，输入：

  ext install cpptools

然后vscode就会联网搜索查找插件列表，然后选择一个评价高的下载安装就好，安装好之后vscode会提示重启，重启即可。

### 安装编译调试环境
目前windows下调试仅支持 Cygwin 和 MinGW。 

我电脑里有安装有MinGW，没有的话上网下一个安装就好。

安装好之后进入MinGW，然后注意一下gdb一定要选上，否则无法调试

![image](https://github.com/Fuyi-Huang/Fuyi-Huang.github.io-vscode-c/raw/master/pictures/capture.JPG)

选中之后右键Make for Installation进行标记，其中gcc和g++为c和c++编译器。

然后配置系统环境变量path，这一步是必须的。

在 我的电脑 上右键属性：

然后做如下操作：

![image](https://github.com/Fuyi-Huang/Fuyi-Huang.github.io-vscode-c/raw/master/pictures/capture1.JPG)


### 修改vscode调试配置文件

打开vscode，**注意配置系统环境变量path后重启一下vscode **

注意vscode调试需要在打开的文件夹中进行

打开文件夹后，新建test.cpp进行输入代码测试： 

如图示进入调试界面选择C++：

![image](https://github.com/Fuyi-Huang/Fuyi-Huang.github.io-vscode-c/raw/master/pictures/capture2.jpg)

![image](https://github.com/Fuyi-Huang/Fuyi-Huang.github.io-vscode-c/raw/master/pictures/capture3.jpg)

然后会在工作目录下的生成一个launch.json的启动配置文件: 

![image](https://github.com/Fuyi-Huang/Fuyi-Huang.github.io-vscode-c/raw/master/pictures/capture4.jpg)

使用下面代码替换该文件：

`
{

    "version": "0.2.0",

    "configurations": [

        {

            "name": "C++ Launch (GDB)",                 // 配置名称，将会在启动配置的下拉菜单中显示

            "type": "cppdbg",                           // 配置类型，这里只能为cppdbg

            "request": "launch",                        // 请求配置类型，可以为launch（启动）或attach（附加）

            "launchOptionType": "Local",                // 调试器启动类型，这里只能为Local

            "targetArchitecture": "x86",                // 生成目标架构，一般为x86或x64，可以为x86, arm, arm64, mips, x64, amd64, x86_64

            "program": "${file}.exe",                   // 将要进行调试的程序的路径

            "miDebuggerPath":"a:\\MinGW\\bin\\gdb.exe", // miDebugger的路径，注意这里要与MinGw的路径对应

            "args": ["blackkitty",  "1221", "# #"],     // 程序调试时传递给程序的命令行参数，一般设为空即可

            "stopAtEntry": false,                       // 设为true时程序将暂停在程序入口处，一般设置为false

            "cwd": "${workspaceRoot}",                  // 调试程序时的工作目录，一般为${workspaceRoot}即代码所在目录

            "externalConsole": true,                    // 调试时是否显示控制台窗口，一般设置为true显示控制台

            "preLaunchTask": "g++"　　                  // 调试会话开始前执行的任务，一般为编译程序，c++为g++, c为gcc

        }

    ]

}
`

这里要**注意miDebuggerPath要与MinGw的路径对应 **

替换后保存，然后切换至test.cpp，按F5进行调试，此时会弹出一个信息框要求你配置任务运行程序，点击它~ 

![image](https://github.com/Fuyi-Huang/Fuyi-Huang.github.io-vscode-c/raw/master/pictures/capture5.jpg)

在这里随便选一个：**这里选择MSBuild的话，你就可以按F5的时候顺便执行生成的程序。**

![image](https://github.com/Fuyi-Huang/Fuyi-Huang.github.io-vscode-c/raw/master/pictures/capture6.jpg)
然后用下面代码替换：

`
{

    "version": "0.1.0",

    "command": "g++",

    "args": ["-g","${file}","-o","${file}.exe"],    // 编译命令参数

    "problemMatcher": {

        "owner": "cpp",

        "fileLocation": ["relative", "${workspaceRoot}"],

        "pattern": {

            "regexp": "^(.*):(\\d+):(\\d+):\\s+(warning|error):\\s+(.*)$",

            "file": 1,

            "line": 2,

            "column": 3,

            "severity": 4,

            "message": 5

        }

    }

}
`
保存一下，然后切换至test.cpp，再次按F5启动调试~ 

![image](https://github.com/Fuyi-Huang/Fuyi-Huang.github.io-vscode-c/raw/master/pictures/capture7.jpg)


撒花!
