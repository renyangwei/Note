# postgres数据库连接

首先得安装postgres数据库，建议使用`docker`

```go
package main

import (
	"database/sql"
	"fmt"
	_ "github.com/lib/pq" //导入数据库驱动
)

var Db *sql.DB

func init() {
	var err error
	Db, err = sql.Open("postgres", "user=gwp dbname=gwp password= host=localhost port=5432 sslmode=disable")
	if err != nil {
		fmt.Println(err.Error())
		return
	}
}

func (post *Post) Create() error {
	statement := "insert into posts (content, author) values ($1, $2) returning id"
	stmt, err := Db.Prepare(statement)
	if err != nil {
		return err
	}
	defer stmt.Close()
	err = stmt.QueryRow(post.Content, post.Author).Scan(&post.Id)
	if err != nil {
		return err
	}
	return nil
}

func main() {
	post := Post{Content: "Hello, Postgres", Author: "Ren"}
	err := post.Create()
	if err != nil {
		fmt.Println(err.Error())
		return
	}
}
```