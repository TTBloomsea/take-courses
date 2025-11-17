```
**REGION 初始参数
# 将下面的AckClose变量，设为False，可以关闭每次切换视频时的确认继续提示
SET AckClose TO $'''True'''
**ENDREGION
Folder.GetSpecialFolder SpecialFolder: Folder.SpecialFolder.DesktopDirectory SpecialFolderPath=> SpecialFolderPath
WebAutomation.LaunchEdge.AttachToTheForegroundEdge AttachTimeout: 5 TargetDesktop: $'''{\"DisplayName\":\"本地计算机\",\"Route\":{\"ServerType\":\"Local\",\"ServerAddress\":\"\"},\"DesktopType\":\"local\"}''' BrowserInstance=> Browser
ON ERROR
    CALL 错误处理
    THROW ERROR
END
IF (WebAutomation.IfWebPageContains.WebPageContainsText BrowserInstance: Browser Text: $'''温馨提示''') THEN
    SET LastError TO $'''UserError:存在提示'''
    CALL 错误处理
END
Display.ShowMessageDialog.ShowMessageWithTimeout Title: $'''准备运行ヾ(≧▽≦*)o''' Message: $'''已捕获到浏览器
要终止脚本运行可以关掉浏览器
(此消息会自动关闭)''' Icon: Display.Icon.Information Buttons: Display.Buttons.OK DefaultButton: Display.DefaultButton.Button1 IsTopMost: True Timeout: 3
CALL 正常播放
```

