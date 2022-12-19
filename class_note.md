# **計概實習上課筆記**

同步更新步驟：
1. git fetch（抓取雲端資料）
2. git diff origin/main（查看不同之處）
3. git pull（同步更新）
-------------------------------------------
【Linux指令】
- cd：變更目錄
-	pwd：顯示目前所在目錄的位置
-	ls：顯示目錄下的所有檔案
-	ls -l：顯示目錄下所有檔案的詳細資訊
-	ls -al：顯示幕錄下所有檔案（包含隱藏檔）的詳細資訊
-	touch：建立空白檔案
  - touch filename
-	cp：複製檔案
  - cp -參數 來源檔案 目標檔案
  - 參數：
    - -p：將檔案本身屬性（權限、所有者、時間）同時複製過去（一般用於備份居多）
    - -r：針對目錄下檔案做遞歸複製（整個目錄下每一個檔案複製到你想要的位置）
    - 例：cp -r dir1 dir2
-	cat：印出檔案內容
	cat filename
	cat file1 file2：將文件內容串接後顯示
-	echo：印出文字
	例：echo “text”
	echo “text” >> filename（將文字寫入filename，用 > 也可以）
-	vi / vim：編輯文檔（後者相當於升級版）
	一般模式：可使用上下左右進行游標移動
	編輯模式：編輯文字、刪除字元及複製貼上檔案資料
。	:w = 存檔
。	:q = 離開
。	:q! = 強制離開不存檔
。	:wq = 存檔後離開
。	:w[filename] = 另存新檔
。	:r[filename] = 在編輯的資料中讀入另一個檔案的資料
。	:n1,n2 w[filename] = 將n1到n2的內容儲存成filename這個檔案
	一般模式 -> 編輯模式：ESC 或 Ctrl + [
	編輯模式 -> 一般模式：
。	i = insert
。	a = append
。	o = new line
-	mkdir：建立一個新目錄
-	mkdir -p：同時建立多個目錄
-	rmdir：刪除一個空目錄
-	rm：刪除檔案
-	rm -r：強制刪除
-	mv：移動、重新命名
-	chown：修改檔案或目錄的擁有者及群組
-	chmod：更改使用者權限
	chomd [擁有者權限][群組權限][其他人權限] filename
	例1：
。	chomd 755 testfile
。	755：[4+2+1][4+1][4+1]
	例2：
。	chomd u=rxw,g=rx,o=rx testfile
。	chomd o+w testfile
。	chomd a-x testfile
。	u=user 擁有者
。	g=group 群組
。	o=other 其他人
。	a=all 全部人
-	nano：編輯文檔
	Ctrl + C：顯示游標所在
	Ctrl + W：查詢命令，按下後會跳轉到末行的反白位置，輸入要查詢的內容再按 enter 即可
-	壓縮檔案：
	gzip
。	壓縮：gzip Filename
。	解壓縮：
	gunzip FileName.gz
	gzip -d FileName.gz
	xz
。	壓縮：xz -z FileName
。	解壓縮：xz -d FileName.xz
	tar.gz
。	壓縮：tar -zcvf FileName.tar.gz DirName
。	解壓縮：tar -zxvf FileName.tar.gz
-	檔案搜尋
	Find [path] [option] [action] filename
。	option：
	-size
	例：-size +500M（找出大於500M的檔案）
	-name
	例：-name “.jpg”（找出照片檔）
	-type
	例1：-type f（一般檔案）
	例2：-type d（一般目錄）
	-user
	例：-user user1 -o -user user2（同時找兩個擁有者的檔案）
	which filename
。	-a：系統會顯示所有被找到的命令執行檔之完整路徑
。	-n<文件名長度>：指定文件名長度，指定的長度必須大於或等於所有文件中最常的文件名
。	-p<文件名長度>：與-n參數相同，但此處的<文件名長度>包含文件的路徑
。	-w：指定輸出欄位的寬度
。	-V：顯示版本訊息
-	

【目錄】
-	. ：此層目錄
-	.. ：上一層目錄
-	- ：前一個工作目錄
-	~ ：「目前使用者身分」的家目錄

【目錄權限】
-	權限設定（drwx）：目錄 / 可讀取 / 可寫入 / 可執行
-	顯示順序：user（擁有者）/ group（群組）/ other
-	r：4   w：2   x：1

【正則表達式 特殊符號】
-	^ ：搜尋規則前的開頭
-	$ ：搜尋規則前的結尾
-	. ：任意一個字元
-	* ：任意字元或字串、單一字元或群組出現任意次數
-	.* ：一起使用代表任意字串
-	+ ：單一字元或群組至少出現一次
-	? ：單一字元或群組至少出現0或1次
-	{n,m} ：比對前一個字元至少n次，最多m次，nm皆為正整數
	例：’a{3,6}’ 為三到六個 ’a’
-	() ：把想找的相關字詞放入括號內，可依照括號內的字元排序找到可能的結果
	例：(sym) -> sympathy、symbol、assym等
-	[] ：比對範圍內的字元或字串
	例：’[a-z]’ 為所有英文字母小寫
-	[^] ：比對不在指定範圍內的字元
-	[-] ：範圍
-	\ ：將任何特殊字元恢復成一般字元

【正則表達式 特定字元】
-	\d ：數字（例：123）
-	\D ：非數字（例：abc或ABC）
-	\w ：數字、字母、底線（例：yes_123或YES123_）
-	\W ：非\w（例：， 或 、 或 -）
-	\s ：空白字元
-	\S ：非空白字元（例：123 或 yes123_ 或 ，）

