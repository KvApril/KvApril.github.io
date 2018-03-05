---
layout: post
title: "ruby_Write_xlsx 创建xlsx文件"
date: 2018-03-03
description: "ruby_Write_xlsx 创建xlsx文件"
tag: Ruby
--- 
### 安装write_xlsx gem
```
gem install 'write_xlsx'
```

### 使用write_xlsx gem来创建xlsx文件
新建xlsx，写入数据
```
require 'rubygems'
require 'write_xlsx'

#新建一个Excel workbook
workbook = WriteXLSX.new('ruby.xlsx')
# Add a worksheet
worksheet = workbook.add_worksheet

# Add and define a format
format = workbook.add_format # Add a format
format.set_bold
format.set_color('red')
format.set_align('center')

# Write a formatted and unformatted string, row and column notation.
col = row = 0
worksheet.write(row, col, "Hi Excel!", format)
worksheet.write(1,   col, "Hi Excel!")

# Write a number and a formula using A1 notation
worksheet.write('A3', 1.2345)
worksheet.write('A4', '=SIN(PI()/4)')


workbook.close
```

### 为xlsx添加样式
```
#cell formatting
def demo_2
    workbook = WriteXLSX.new('cell.xlsx')
    worksheet1 = workbook.add_worksheet 'sheet1'
    worksheet2 = workbook.add_worksheet 'sheet2'

    format1 = workbook.add_format #add a format
    format2 = workbook.add_format #add a format

    format1.set_bold
    format1.set_color('green')
    format1.set_bg_color('pink')

    format2.set_bold
    format2.set_color('red')

    #工作目录1
    worksheet1.write(0,0,"one",format1)
    worksheet1.write_string(1,0,'two',format1)
    worksheet1.write_number(2,0,3,format1)
    worksheet1.write_blank(3,0,format1)
    worksheet1.set_row(4,10,format1)#指定行 第一个参数是行，第二个参数是行宽
    worksheet1.set_column(5,3,15,format1)#指定结束列，开始列，列宽，样式

    worksheet2.write(0,0,"A",format2)
    worksheet2.write_string(1,0,'B',format2)
    worksheet2.write_number(2,0,4,format2)
    worksheet2.write_blank(3,0,format2)
    worksheet2.set_row(4,1,format2)#指定行 第一个参数是行，第二个参数是行宽
    worksheet2.set_column(5,5,15,format2)#指定结束列，开始列，列宽，样式

    #properties
    format3 = workbook.add_format(:bold=>1,:color=>"yellow",:font=>12)
    format4 = workbook.add_format
    format4.set_format_properties(:bold=>3,:color=>"pink",:font=>12)
    worksheet1.write(7,0,'sssss',format3)
    worksheet1.write(8,0,'aaaaa',format4)

    #hash 格式
    font = {
        :font => 'Calibri',
        :size => 16,
        :color => 'blue',
        :bold => 2
    }
    shading = {
        :bg_color => 'green',
        :pattern => 2
    }
    format5 = workbook.add_format(font)
    format6 = workbook.add_format(font.merge!(shading))
    worksheet1.write(9,0,'bbbbb',format5)
    worksheet1.write(10,0,'ccccc',format6)

    workbook.close

end
```

其他样式方法

```
Category   Description       Property        Method Name
--------   -----------       --------        -----------
Font       Font type         font            set_font()
           Font size         size            set_size()
           Font color        color           set_color()
           Bold              bold            set_bold()
           Italic            italic          set_italic()
           Underline         underline       set_underline()
           Strikeout         font_strikeout  set_font_strikeout()
           Super/Subscript   font_script     set_font_script()
           Outline           font_outline    set_font_outline()
           Shadow            font_shadow     set_font_shadow()

Number     Numeric format    num_format      set_num_format()

Protection Lock cells        locked          set_locked()
           Hide formulas     hidden          set_hidden()

Alignment  Horizontal align  align           set_align()
           Vertical align    valign          set_align()
           Rotation          rotation        set_rotation()
           Text wrap         text_wrap       set_text_wrap()
           Justify last      text_justlast   set_text_justlast()
           Center across     center_across   set_center_across()
           Indentation       indent          set_indent()
           Shrink to fit     shrink          set_shrink()

Pattern    Cell pattern      pattern         set_pattern()
           Background color  bg_color        set_bg_color()
           Foreground color  fg_color        set_fg_color()

Border     Cell border       border          set_border()
           Bottom border     bottom          set_bottom()
           Top border        top             set_top()
           Left border       left            set_left()
           Right border      right           set_right()
           Border color      border_color    set_border_color()
           Bottom color      bottom_color    set_bottom_color()
           Top color         top_color       set_top_color()
           Left color        left_color      set_left_color()
           Right color       right_color     set_right_color()
           Diagional type    diag_type       set_diag_type()
           Diagional border  diag_border     set_diag_border()
           Diagional color   diag_color      set_diag_color()
```
