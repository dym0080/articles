
步骤如下：

1. 开始－＞设置－＞控制面板－＞管理工具－＞服务 停止所有Oracle服务。

2. 开始–>所有程序–>Oracle–>Oracle安装产品–>Universal Installer 
“欢迎使用”界面启动后，卸载产品–>展开Oracle主目录下的OraDb11g_home1–>勾选Oracle Database 11g11.2.0.1.0–>删除–>在弹出的确认窗口中选择“是”。卸载完成后，在弹出的“产品清单”界面中选择“关闭”，然后在“欢迎使用”界面中选择“取消”来退出界面。

3. 运行regedit，选择HKEY_LOCAL_MACHINE\SOFTWARE\ORACLE，按del键删除这个入口。

4. 运行regedit，选择HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services，滚动这个列表，删除所有Oracle入口(以oracle或OraWeb开头的键)。

5. 运行refedit，HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Eventlog\Application，删除所有Oracle入口。

6. 删除HKEY_CLASSES_ROOT目录下所有以Ora、Oracle、Orcl或EnumOra为前缀的键。

7. 删除HKEY_CURRENT_USER/Software/Microsoft/Windows/CurrentVersion/Explorer/MenuOrder/Start menu/Programs中以Oracle开头的键

8. 删除HKEY_LOCAL_MACHINE/SOFTWARE/ODBC/ODBCINST.INI中除MicrosoftODB forOracle以外的所有韩Oracle的键

9. 我的电脑-->属性-->高级-->环境变量,删除环境变量CLASSPATH和PATH中有关Oracle的设定。

10. 从桌面上、STARTUP（启动）组、程序菜单中，删除所有有关Oracle的组和图标。

11. 删除所有与Oracle相关的目录(如果删不掉，重启计算机后再删就可以了)包括：
    - C:\Program file\Oracle目录。
    - C:\WINDOWS\system32\config\systemprofile\Oracle目录。
    - C:\Users\Administrator\Oracle或C:\Documents and Settings\Administrator\Oracle目录
    - C:\WINDOWS下删除以下文件ORACLE.INI、oradim73.INI、oradim80.INI、oraodbc.ini等等。
    - C:\WINDOWS下的WIN.INI文件中若有[ORACLE]的标记段，删除该段。

(完)