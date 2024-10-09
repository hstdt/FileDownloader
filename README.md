# FileDownloader

FileDownloader依赖于Alamofire的简单实用封装,只负责处理文件的下载,支持group和queue下载，默认group下载

## 使用

1. 通过Swift Package Manager在Package.swif添加依赖
    ```
    dependencies: [
        .package(url: "https://github.com/lidongx/FileDownloader.git", .upToNextMajor(from: "1.0.0"))
    ]
    ```

## 使用示例

1. 日志输出：

    ```swift
    FileDownloader.shared.enableLog = true
    ```
    
2. 下载调用:
    
    ```swift
    "http://127.0.0.1:8000/back_lunges_with_knee_ups_left_2.mp3".startDownload()
    ```
3. 支持一组URL下载(同时下载):

    ```swift
    [
        "http://127.0.0.1:8000/back_lunges_with_knee_ups_left_2.mp3",
        "https://raw.githubusercontent.com/lidongx/resource/refs/heads/main/back_lunges_with_knee_ups_left_2.mp3"
    ].startDownload()
    ```
4. 支持队列顺序下载(按照先后顺序下载)

    ```swift
    [
        "http://127.0.0.1:8000/back_lunges_with_knee_ups_left_2.mp3",
        "https://raw.githubusercontent.com/lidongx/resource/refs/heads/main/back_lunges_with_knee_ups_left_2.mp3"
    ].startQueueDownload()
    ```
    
5. 更改保存文件名以及文件夹目录

    ```swift
    "http://127.0.0.1:8000/back_lunges_with_knee_ups_left_2.mp3".savedFileName("mm.mp3").folderName("FolderName").startDownload()
    
    [
        "http://127.0.0.1:8000/back_lunges_with_knee_ups_left_2.mp3".savedFileName("mm.mp3").folderName("FolderName"),
        "https://raw.githubusercontent.com/lidongx/resource/refs/heads/main/back_lunges_with_knee_ups_left_2.mp3".fileInfo()
    ].startDownload()
    ```
    
6. 下载配置(单个URL配置和group和queue配置)
   
    ```swift
    "http://127.0.0.1:8000/back_lunges_with_knee_ups_left_2.mp3".fileInfo().config(config:.defaultConfiguration).startDownload()
    ```
    
7. 设置回调代理

   ```swift
      [
         "http://127.0.0.1:8000/back_lunges_with_knee_ups_left_2.mp3".savedFileName("mm.mp3").folderName("FolderName"),
          "https://raw.githubusercontent.com/lidongx/resource/refs/heads/main/back_lunges_with_knee_ups_left_2.mp3".fileInfo()
      ].startDownload(delegate: .init(onFinished: { group, fileInfos in
            
      }, onFailed: { group, errorString in
            
      }, onProgress: { group, progress in
            
      }))
    ```

8. 取消所有的下载

    ```swift
    FileDownloader.shared.cancelAll()
   ```

9. queue和group的取消暂停和恢复下载

  ```swift
  	let group = FileDownloadGroup(urlStrings: [
            "http://127.0.0.1:8000/back_lunges_with_knee_ups_left_2.mp3"
        ], folderConfig: .init(), config: .defaultConfiguration, delegate: nil)
        group.startDownload()
        group.pause()
        group.resume()
        group.cancel()
     
        let queue = FileDownloadQueue(urlStrings: [
            "http://127.0.0.1:8000/back_lunges_with_knee_ups_left_2.mp3"
        ])
        queue.startDownload()
        queue.pause()
        queue.resume()
        queue.cancel()
   ```

 
    