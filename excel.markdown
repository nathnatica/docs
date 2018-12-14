

###### get time(date) stamp value (use when date diff needed)  
(ex) 2018/12/10 16:45:57.187  
=DATEVALUE(A1) + TIMEVALUE(A1)  

###### split string until character(:)  
=LEFT(A1,FIND(":",A1)-1)  

###### make cell ref with function  
=VLOOKUP(INDIRECT("A" & ROW()),Sheet4!$B$1:$C$10,2,FALSE)  

###### coloring entire row by condition  
1. ルール反映領域選択
2. 条件付き書式⇒新しいルール
3. 書式を使用して、書式設定するセルを決定
4. 数式に
= $A1=TRUE
の形で入力する(※columnに$を削除すること)
