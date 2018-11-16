#### 下午写文件上传，写错了方法，写成了fileReader，fileReader是用来读取文件的
* csv可以用js读取，csv就是简单的文本，可以用excel打开.csv使用换行符分隔行，逗号分隔列。读取csv的代码如下
```
<input  type="file"/>
var files = e.target.files;
var file = files[0];
// try sending
var reader = new FileReader();
reader.onloadstart = function() {
// 这个事件在读取开始时触发
    console.log("onloadstart");
}
reader.onprogress = function(p) {
// 这个事件在读取进行中定时触发
   console.log("onprogress");
   // document.getElementById("bytesRead").textContent = p.loaded;
}
reader.onload = function() {
  // 这个事件在读取成功结束后触发
  console.log("load complete");
}
reader.onloadend = function() {
  // 这个事件在读取结束后，无论成功或者失败都会触发
  if (reader.error) {
     console.log(reader.error);
  } else {
  // var data = [].push(csv2array(reader.result.toString()));
  document.getElementById("demo").innerHTML= reader.result.toString();
  }
};
reader.readAsBinaryString(file);
```
* 读取excel文件的成本有点大，可以使用sheetjs库，还可以使用node的开源库
* 正确的上传文件的方法是设置FormData对象，代码如下
```
var form = new FormData();
form.append('filePart', files[0]);
var config = {
  // onUploadProgress: progressEvent => {
  // var complete = (progressEvent.loaded / progressEvent.total * 100 | 0) + '%'
  // this.progress = complete
 // }
};
axios.post(`${get_new_basic_api_url()}/apps/${_this.appId}/intents/upload`,
  form, config).then((res) => {
      console.log(res);
     if (res.status === 200) {
        this.$message.success('上传成功！');
        //更新页面
        let data = res.data;
        console.log(data);
        this.$set(this, 'intentArr', data.concat(_this.intentArr));
     }else{
        this.$message.warning(res.data.message);
     }
})
```
