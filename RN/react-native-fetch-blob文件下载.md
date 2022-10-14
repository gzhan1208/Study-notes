## 因为有个pdf文件分享的需求，时间也不充裕，又没有现成的分享组件，所以把接口传回的二进制流写入到本地文件中，然后手动去分享
### `react-native-fetch-blob` 写入
```javascript
// write UTF8 data to file
RNFetchBlob.fs.writeFile(PATH_TO_WRITE, 'foo', 'utf8')
              .then(()=>{ ... })
// write bytes to file
RNFetchBlob.fs.writeFile(PATH_TO_WRITE, [102,111,111], 'ascii')
              .then(()=>{ ... })
// write base64 data to file
RNFetchBlob.fs.writeFile(PATH_TO_WRITE, RNFetchBlob.base64.encode('foo'), 'base64')
              .then(()=>{ ... })
// write file using content of another file
RNFetchBlob.fs.writeFile(PATH_TO_WRITE, PATH_TO_ANOTHER_FILE, 'uri')
```

### 写入成功后也可以打开本地文件，或者唤起打开方式
```javascript
Android & IOS
RNFetchBlob.ios.openDocument(downPath)

// pdf: 'application/pdf'
RNFetchBlob.android.actionViewIntent(downPath, type)
```

### 如果写入失败了，可以使用 `RNFetchBlob.fs.unlink(downPath)` 将未完成的文件给删除掉
