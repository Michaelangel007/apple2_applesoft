# Mirror of Jamtronix's HTML Applesoft Source

Bob Sander-Cederlof has an excellent reverse engineered Applesoft assembly source:
http://www.txbobsc.com/scsc/scdocumentor/

Jamtronix wrote a ruby script to put this all into one file and link all the functions.
http://jamtronix.com/2013/04/10/applesoft-disassembly/

```ruby
html="<PRE>"
$<.each_line do |line|
 line.gsub!('<','&lt;')
 if line=~/^....-.{21} [J|B]...([A-Z]\S+)\s/
 dest_label=$1
 line[31,dest_label.length]="<a href=\##{dest_label}>#{dest_label}</a>"
 end

 if (!line.include?(" .EQ ") && (line=~/^.{20}([A-Z]\S+)\s/))
 this_label=$1
 line[20,this_label.length]="<b><a name='#{this_label}' id='#{this_label}'>#{this_label}</a></b>"
 end
 line[15,4]="" if line[15,4]=~/\d\d\d\d/
 html+="#{line}" unless line=~/^\s+SAVE /
end
html+="</PRE>"
puts html
```

Unfortunately, his [consolidated and cross-linked version.](http://jamtronix.com/files/applesoft.html) is no longer available.
Thankfully, The WayBackMachine has a [mirror copy](https://web.archive.org/web/20131106182736/http://jamtronix.com/files/applesoft.html).

But in case that goes away here is a git repo [mirror](https://htmlpreview.github.io/?https://github.com/Michaelangel007/apple2_applesoft/blob/master/applesoft.html)
