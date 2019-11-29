package main

import (
	"database/sql"
	"fmt"
	_ "github.com/go-sql-driver/mysql"
)
type  DbWorker struct {
//mysql data source name
	ID int "json:'id'"
	Dsn string
}

func main() {
	szs := DbWorker{
		Dsn: "root:@tcp(127.0.0.1:3306)/szs",
	}
	db, err := sql.Open("mysql", szs.Dsn)
	if err != nil {
		panic(err)
	}else {
		fmt.Println("连接数据库成功")
	}
	defer db.Close()


	//创建
	result,err := db.Exec("INSERT INTO szs20191126(test_id,test_name) VALUES (?,?)",7,"6666")
	if err != nil{
		fmt.Println("insert failed,",err)
	}
	// 通过LastInsertId可以获取插入数据的id
	testId,err:= result.LastInsertId()
	// 通过RowsAffected可以获取受影响的行数
	testName,err:=result.RowsAffected()
	fmt.Println("test_id:", testId)
	fmt.Println("test_name:", testName)



	//查询
	rows,err := db.Query("select test_id,test_name from szs20191126 where test_id > 3" )
	if err != nil{
		fmt.Println("select db failed,err:",err)
		return
	}
	for rows.Next(){
		var s string
		var ss string
		err = rows.Scan(&s,&ss)
		if err != nil {
			fmt.Println(err)
			return
		}
		fmt.Println(s,ss)
	}

	//删除数据
	results,err := db.Exec("DELETE from szs20191126 where test_id=?",7)
	if err != nil{
		fmt.Println("delete data fail,err:",err)
		return
	}
	fmt.Println(results.RowsAffected())



}

//func DBWorker(db *sql.DB)  {
//	DNS:="root:@tcp(127.0.0.1:3306)/szs?charset=utf-8"
//db,err:=sql.Open("mysql",DNS)
//	defer db.Close()
//}

