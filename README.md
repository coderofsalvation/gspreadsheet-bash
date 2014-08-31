gspreadsheet-bash
=================

portable google spreadsheet bash client which lets you combine your unix-fu with spreadsheets. Piping/replacing spreadsheet from the console for lazy developers :)

# Usage 
       
    gspreadsheet <export|import> <spreadsheetname> <sheetgid> <type>

    types: are 'xls' 'csv' 'pdf' 'ods' 'tsv' 'ods' or 'html'

    $ user=my@email.com pass=googlepasswd gspreadsheet export 'My spreadsheet' 12323
    $ echo "foo\tflop" | user=my@email.com pass=googlepasswd gspreadsheet import 'My spreadsheet' 12323
    $ echo '"foo","bar"' | user=my@email.com pass=googlepasswd gspreadsheet import 'My spreadsheet' 12323 csv


The sheetgid can be found in the googlespreadsheet browserurl.
These urls end with '#gid=123' (so 123 is the sheetgid).

# Example: Spreadsheet to console
  
    user=my@email.com pass=googlepasswd gspreadsheet export 'My spreadsheet' 12323
    foo4   bar4
    foo1   bar1
    foo2   bar3

Now you can go crazy with sed, awk and your shell-fu!

# Example: Spreadsheet to .XXX
  
    user=my@email.com pass=googlepasswd gspreadsheet export 'My spreadsheet' 12323 pdf > report.pdf
    user=my@email.com pass=googlepasswd gspreadsheet export 'My spreadsheet' 12323 csv > report.csv

Now you can go crazy with cron and load data in your application.

# Example: Search/Replace 

    $ export user="my@email.com"
    $ export pass="owerwer"
    $ gspreadsheet export "My spreadsheet" 123 | sed 's/flip/flop/g' | gspreadsheet import "My spreadsheet" 123

# Example: Mysql-table to spreadsheet

    $ export user="my@email.com"
    $ export pass="owerwer"
    $ echo "select * from users" | mysql -uusername -ppassword db_name | gspreadsheet import 'My spreadsheet' 123

# Example: Import Console-fu

    $ export user="my@email.com"
    $ export pass="owerwer"
    $ ls -la | awk '{ for(i = 1; i <= NF; i++) { printf "%s",$i; if( i < NF ) printf "\t" }; printf "\n" }' | gspreadsheet import "My spreadsheet" 123

The awk oneliner converts the usual spacedelimited unix output to tsv (tabseperated fields, the format which our gspreadsheet utility likes).

  <img alt="" src=".res/example.png"/>

# Todos

* add row function (import fully overwrites sheet)

Strangely enough the gspreadsheet api v3 does not simply allow adding rows without knowing the columnnames. Quite a pity, because it makes thing much more complex to implement.

# Requirements

* any linux distro (bash+curl+gawk)
