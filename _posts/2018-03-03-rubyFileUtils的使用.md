---
layout: post
title: "ruby_FileUtils的使用"
date: 2018-03-03
description: "ruby_FileUtils的使用"
tag: Ruby
--- 
### 文件操作
```
Dir['*.rb'] #basic globs
Dir['**/*.rb'] #** == any depth of directory, including current dir.
#=> array of relative names

File.expand_path('~/file.txt') #=> "/User/mat/file.txt"
File.dirname('dir/file.txt') #=> 'dir'
File.basename('dir/file.txt') #=> 'file.txt'
File.join('a', 'bunch', 'of', 'strings') #=> 'a/bunch/of/strings'

__FILE__ #=> the name of the current file
2.3.3 :057 > puts __FILE__
(irb)
 => nil
```

### FileUtils 常用方法

```
require 'fileutils' #load fileutils
include FileUtils  # Gives you access (without prepending by 'FileUtils.') to
cd(dir, options)
cd(dir, options) {|dir| .... }
pwd()
mkdir(dir, options)
mkdir(list, options)
mkdir_p(dir, options)
mkdir_p(list, options)
rmdir(dir, options)
rmdir(list, options)
ln(old, new, options)
ln(list, destdir, options)
ln_s(old, new, options)
ln_s(list, destdir, options)
ln_sf(src, dest, options)
cp(src, dest, options)
cp(list, dir, options)
cp_r(src, dest, options)
cp_r(list, dir, options)
mv(src, dest, options)
mv(list, dir, options)
rm(list, options)
rm_r(list, options)
rm_rf(list, options)
install(src, dest, mode = <src's>, options)
chmod(mode, list, options)
chmod_R(mode, list, options)
chown(user, group, list, options)
chown_R(user, group, list, options)
touch(list, options)
```
