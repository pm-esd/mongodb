```golang
package main

import (
	"fmt"

	"github.com/pm-esd/mongodb"
	"go.mongodb.org/mongo-driver/bson"
)

func main() {
	mongo := &mongodb.Config{
		Url:             "mongodb://127.0.0.1:37017",
		Database:        "admin_request_log",
		MaxConnIdleTime: 5,
		MaxPoolSize:     1000,
		Username:        "",
		Password:        "",
	}

	mongo.NewClient()

	res := mongo.Collection("request_log").InsertOne(bson.M{"name": "pi", "value": 3.14159})

	fmt.Println(res)

	var result struct {
		Value float64
	}

	err := mongo.Collection("request_log").Where(bson.M{"name": "pi"}).FindOne(&result)
	if err != nil {
		fmt.Println(err)
	}
	fmt.Println(result)

}
```