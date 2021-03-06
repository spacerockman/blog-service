# blog-service

## get started with the offical document

+ https://gin-gonic.com/docs/quickstart/

# design a structure of a new go program

```blog-service_structure
├── configs
├── docs
├── global
├── internal
│   ├── dao
│   ├── middleware
│   ├── model
│   ├── routers
│   └── service
├── pkg
├── storage
├── scripts
└── third_party
```

# design the DB for this project
blog_service.db

# design the api

## 1. manage tags
| functions               | HTTP methos | path      |
| ----------------------- | ----------- | --------- |
| add tag                 | POST        | /tags     |
| delete the specific tag | DELETE      | /tags/:id |
| update the specific tag | PUT         | /tags/:id |
| get list of tags        | GET         | /tags     |

## 2. manage articles
| functions                   | HTTP methos | path          |
| --------------------------- | ----------- | ------------- |
| add article                 | POST        | /articles     |
| delete the specific article | DELETE      | /articles/:id |
| update the specific article | PUT         | /articles/:id |
| get the specific articel    | GET         | /articles/:id |
| get the list of articles    | GET         | /articles     |

# design routers
+ design methos of routers
+ /routers/api/v1/router.go (common)
+ /routers/api/v1/Tag.go
+ /routers/api/v1/Article.go
  
```
├── README.md
├── blog_service.db
├── configs
├── docs
├── global
├── go.mod
├── go.sum
├── internal
│   ├── dao
│   ├── middleware
│   ├── model
│   │   ├── article.go
│   │   ├── article_tag.go
│   │   ├── model.go
│   │   └── tag.go
│   ├── routers
│   │   ├── api
│   │   │   └── v1
│   │   │       ├── Article.go
│   │   │       └── Tag.go
│   │   └── router.go
│   └── service
├── main.go
├── pkg
├── scripts
├── storage
└── third_party
```
# design common components

## 1. error code
+ pkg/errcode/common_code.go -- common error code
+  pkg/errcode/errcode.go -- deal with errors

## 2. configuration
+ $ go get -u github.com/spf13/viper@v1.4.0 -- install viper
+ configs/config.yaml

## 3. componnets
+ pkg/setting/setting.go --↑used for read the configuration
+ pkg/setting/section.go --↑used for read the configuration

## 4. connect configuration with the application
+ global/setting.go

## 5. initialize and read the configuration
+ main.go
  + init()
  + setupSetting()

```
├── README.md
├── blog_service.db
├── configs
│   └── config.yaml
├── docs
├── global
│   └── setting.go
├── go.mod
├── go.sum
├── internal
│   ├── dao
│   ├── middleware
│   ├── model
│   │   ├── article.go
│   │   ├── article_tag.go
│   │   ├── model.go
│   │   └── tag.go
│   ├── routers
│   │   ├── api
│   │   │   └── v1
│   │   │       ├── Article.go
│   │   │       └── Tag.go
│   │   └── router.go
│   └── service
├── main.go
├── pkg
│   ├── errorcode
│   │   ├── common_code.go
│   │   └── errcode.go
│   └── setting
│       ├── section.go
│       └── setting.go
├── scripts
├── storage
└── third_party
```

## 6. connetc to Database
  1. go get -u github.com/jinzhu/gorm@v1.9.12 --with gorm
  2. internal/model/model.go -----> NewDBEngine()
  3. initialize mysql
     + go get github.com/jinzhu/gorm/dialects/mysql
     + global/ -------> db.go
  4. main.go ------> setupDBEngine()