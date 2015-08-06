1. 把package.json，Gruntfile.js放到项目文件夹下
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

Gruntfile.js

```javascript
module.exports = function (grunt) {
    // 项目配置
    grunt.initConfig({
        pkg: grunt.file.readJSON('package.json'),
        uglify: {
            // uglify的任务target1
            target1: {
                src: 'src/1.js',
                dest: 'dest/1.min.js'
            }
        },
        concat: {
            options: {
                separator: ';'
            },
            // concat的任务target1
            target1: {
                src: ['src/a.js', 'src/b.js'],
                dest: 'dest/c.js'
            },
            // concat的任务target2
            target2: {
                src: ['src/d.js', 'src/e.js'],
                dest: 'dest/f.js'
            }
        }
    });

    grunt.loadNpmTasks('grunt-contrib-uglify');
    grunt.loadNpmTasks('grunt-contrib-concat');
    
    // 先执行uglify任务，再执行concat任务
    grunt.registerTask('default', ['uglify', 'concat']);
};
```

**文件对象格式**

这种形式支持每个目标对应多个src-dest形式的文件映射，属性名就是目标文件，源文件就是它的值(源文件列表则使用数组格式声明)。可以使用这种方式指定数个src-dest文件映射， 但是不能够给每个映射指定附加的属性。

```javascript
module.exports = function (grunt) {
    // 项目配置
    grunt.initConfig({
        pkg: grunt.file.readJSON('package.json'),
        uglify: {
            // uglify的任务target1
            target1: {
                files: {
                    'dest/app1.min.js': ['src/1.js', 'src/2.js'],    //把1.js, 2.js压缩后合并到app1.min.js
                    'dest/app2.min.js': ['src/3.js', 'src/4.js']     //把3.js, 4.js压缩后合并到app2.min.js
                }
            }
        },
        concat: {
            options: {
                separator: ';'
            },
            // concat的任务target1
            target1: {
                files: {
                    'dest/c.js': ['src/a.js', 'src/b.js'],   //把a.js,b.js合并成c.js
                    'dest/f.js': ['src/d.js', 'src/e.js']    //把d.js,e.js合并成f.js
                }
            }
        }
    });

    grunt.loadNpmTasks('grunt-contrib-uglify');
    grunt.loadNpmTasks('grunt-contrib-concat');
    
    // 先执行uglify任务，再执行concat任务
    grunt.registerTask('default', ['uglify', 'concat']);
};
```

