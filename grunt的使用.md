1. 把package.json放到项目文件夹下
2. 执行npm install会根据json下载相应的文件到项目目录下


package.json:

```json
{
  "name": "my-project-name",
  "description": "my-project-name",
  "version": "0.1.0",
  "devDependencies": {
    "grunt": "^0.4.5",
    "grunt-contrib-concat": "^0.5.1",
    "grunt-contrib-jshint": "^0.11.2",
    "grunt-contrib-nodeunit": "^0.4.1",
    "grunt-contrib-uglify": "^0.9.1",
    "grunt-contrib-watch": "^0.6.1"
  }
}
```
