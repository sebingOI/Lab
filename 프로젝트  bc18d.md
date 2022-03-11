# 프로젝트 로그인 구현

> config.json 부분
> 

```jsx
{
  "development": {
    "username": "root",
    "password": "1234",
    "database": "node.js",
    "host": "127.0.0.1",
    "dialect": "mysql"
  },
  "test": {
    "username": "root",
    "password": null,
    "database": "database_test",
    "host": "127.0.0.1",
    "dialect": "mysql"
  },
  "production": {
    "username": "root",
    "password": null,
    "database": "database_production",
    "host": "127.0.0.1",
    "dialect": "mysql"
  }
}
```

> index부분
> 

```jsx
const Sequelize = require('sequelize');
const User = require('./user');

const env = process.env.NODE_ENV || 'development';
const config = require('../config/config')[env];
const db = {};

const sequelize = new Sequelize(config.database, config.username, config.password, config);
db.sequelize = sequelize;

db.User = User;

User.init(sequelize);

User.associate(db);

module.exports = db;
```

> user부분
> 

```jsx
const Sequelize = require('sequelize');

module.exports = class User extends Sequelize.Model{
    static init (sequelize) {
        return super.init({
            email: {
                type: Sequelize.STRING(20),
                allowNull : false,
                unique: true,
            },
            password: {
                type: Sequelize.TEXT,
                allowNull: true,
            },
            nickname:{
                type: Sequelize.STRING(20),
                allowNull: true,
            }
        }, {
            sequelize,
            timestamps:false,
            underscored:false,
            modelName:'User',
            tableName:'users',
            paranoid: false,
            charset: 'utf8',
            collate: 'utf8_general_ci',
        });
    }
    static associate(db) {}
}
```

> index.html
> 

```jsx
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    <title>Document</title>
</head>
<body>
    <script>
        const email = "qwer";
        const password = "asdf";
        const nickname = "bin"
        const data = {
            email,
            password
        };
        axios.post("127.0.0.1:8002",data ).then((res) => {
            console.log(res);
        })
    </script>
</body>
</html>
```

> app.js
> 

```jsx
const express = require('express');
const path = require('path');
const morgan = require('morgan');
const nunjucks = require('nunjucks');
//const User = require('User');
const db = require('./models');
const { sequelize, User } = require('./models');
const { request } = require('https');
const mysql = require("mysql");

// const req = require('express/lib/request');

const app = express();
app.set('port', process.env.PORT || 8002);
app.set('view engine', 'html');
nunjucks.configure('view', {
    express: app,
    watch: true,
});
sequelize.sync({ force: false })
    .then(() => {
        console.log('데이터베이스 연결 성공');
    })
    .catch((err) => {
        console.error(err);
    });

app.use(morgan('dev'));
app.use(express.static(path.join(__dirname, 'public')));
app.use(express.json());
app.use(express.urlencoded({ extended: false }));

app.use((err, req, res, next) => {
    res.locals.message = err.message;
    res.locals.error = process.env.NODE_ENV !== 'production' ? err : {};
    res.status(err.status || 500);
    res.render('error');
});

// 통신처리(조회)
app.post('/', async(req, res) => {
    try {
        const user = await User.findOne({
            where: {
                email: req.body.email 
            }
        })
        if (user) {
            if (req.body.password == user.password) {
               // res.json({ nickname: user[0].nickname });
               res.send(user.nickname);
            }
            else { res.send("failed"); }
        } else { res.send("failed"); }
    } catch(err) {
        console.error(err);
    }
    console.log(req.body);
});

app.post('/create', async(req, res) => {
    try {
        const user = await User.create({
            email: req.body.email,
            password: req.body.password,
            nickname: req.body.nickname,
        });
        res.send("회원가입 성공");
        console.log(User);
    } catch(err) {
        res.send("회원가입 실패");
        console.log(User);
        console.error(err);
    }
});

app.post('/update', async(req, res) => {
    try {
        const user = await User.update({
            password : req.body.password,
            nickname : req.body.nickname,
        }, {
            where: {
                email: req.body.email
            }
        });
        res.send("회원 정보 수정 성공");
    } catch(err) {
        res.send("회원 정보 수정 실패");
        console.error(err);
    }
});

app.post('/delete', async(req, res) => {
    try {
        const user = await User.destroy({
            where: { 
                email: req.body.email,
                password: req.body.password,
                nickname: req.body.nickname,
            }
        });
        res.send("회원 정보 삭제 성공");
    } catch(err) {
        res.send("회원 정보 삭제 실패");
        console.error(err);
    }
});

app.listen(app.get('port'), () => {
    console.log(app.get('port'), '번 포트에서 대기 중');
});
```

> pakage.json
> 

```jsx
{
  "name": "1222",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node app.js"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "cors": "^2.8.5",
    "express": "^4.17.2",
    "morgan": "^1.10.0",
    "mysql": "^2.18.1",
    "mysql2": "^2.3.3",
    "nunjucks": "^3.2.3",
    "require": "^2.4.20",
    "sequelize": "^6.12.1",
    "sequelize-cli": "^6.3.0"
  },
  "devDependencies": {
    "nodemon": "^2.0.15"
  }
}
```