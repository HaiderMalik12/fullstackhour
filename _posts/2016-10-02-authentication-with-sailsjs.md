---
layout: dark-post
title: "Authentication with Sails.js"
description: "JWT Authentication with Sails.js"
tags: [Node.js, Sails.js]
categories: [Sails.js, Node.js]
comments: true
image:
    feature: sails-logo.jpg
share: true
---
<div style="text-align:center;">
<button class="btn btn-primary btn-lg" >
<a href="https://github.com/HaiderMalik12/sails-auth-app/tree/feature-signup-school" target="_blank">Code</a>
</button>
</div>


<h2 class="section-heading">What is Sails.Js ?</h2>


<p>Sails makes it easy to build custom, enterprise-grade Node.js apps. It is designed to emulate the familiar MVC pattern of frameworks like Ruby on Rails, but with support for the requirements of modern apps: data-driven APIs with a scalable, service-oriented architecture. It's especially good for building chat, realtime dashboards, or multiplayer games; but you can use it for any web application project - top to bottom.</p>

<h2 class="section-heading">What we Build: A School Listing App</h2>

<ul>
 <li>School or Teacher can create a new Account</li>
 <li>School or Teacher can login to his Account</li>
  <li>As an authenticated School or Teacher, Teacher can view his profile</li>
 </ul>

<h2 class="section-heading">Exploring the Directory Structure</h2>


<br>

<pre class=" language-javascript"><code class=" javascript language-javascript">
├── api
│   ├── controllers
│   ├── models
│   ├── policies
│   ├── responses
│   └── services
├── assets
│   ├── images
│   ├── js
│   │   └── dependencies
│   ├── styles
│   └── templates
├── config
│   ├── env
│   └── locales
├── node_modules
│   ├── ejs
│   ├── grunt
│   ├── grunt<span class="token operator">-</span>contrib<span class="token operator">-</span>clean
│   ├── rc
│   ├── sails
│   └── sails<span class="token operator">-</span>disk
├── tasks
│   ├── config
│   └── register
└── views
</code></pre>

<ul>
<li><strong>Models</strong> query your database and return the necessary data.</li>
<li><strong>Views</strong> are pages that render data. In SailsJs, they are <code>.ejs</code> template files.</li>
<li><strong>Controllers</strong> handle user requests, retrieve data from the models and pass them on to the views.</li>
<li><strong>Policies</strong> are used to restrict access to certain parts of your app. It can be used for anything: HTTP Basic Auth, 3rd party Single Sign on, OAuth 2.0 or your own custom authorization scheme.
<strong> Services</strong> are more like helpers that you can write once and use anywhere in your app. They are globalised by default, so you don’t need to require them. </li>
<li><a href="http://sailsjs.org/documentation/anatomy/my-app" target="_blank">Get More Details</a>.</li>
</ul>


<h2 class="section-heading">Installation and Configuration</h2>



<p>In order to install sails in your computer, make sure you have the
lastest version of Node and npm installed.</p>

<p> Run the following command to install it.</p>

`
   npm install -g sails
`

<p>If you are using Linux or Mac osx, Run the following command</p>

 `
   sudo npm install -g sails
 `

<p>Once it is installed, we can create a new app from command line like so:</p>

```bash
   sails new auth-app
   cd auth-app
   sails lift
 ```

 <p><code>sails lift</code> starts web server and points you to the url
 where the app is currently been server.By default sails uses port 1337 to lift this app.</p>

<p>Get more details about the anatomy of a sails app <a href="http://sailsjs.org/documentation/anatomy/my-app/api" target="_blank">here</a></p>


<h2 class="section-heading">Setting Up database Configurations</h2>

<p>Sails provides many adapters like Mysql, Mongodb and Redis Get more details about adapters <a href="http://sailsjs.org/documentation/concepts/models-and-orm">here</a></p>

<p>If you have installed Mysql workbench.Create a schema or database in Mysql workbench. I have created a databse called <code>funrun-api</code> </p>

<p>We are going to use mysql adapter. We have to install it first by running this command</p><code> npm install --save sails-mysql </code>

<p>Create a connection in your development.js</p>

```js

 //config/env/development.js
module.exports = {


  connections: {

    mysqlServer: {
      adapter: 'sails-mysql',
      user: 'root',
      password: 'root',
      database: 'funrun_api',
      port:3306,
      host  : '127.0.0.1'
      //socketPath : '/tmp/mysql.sock'
    }


  },


  models: {
    connection: 'mysqlServer'
  },


  port: 1337,
  // LOG_QUERIES: 'true',
  // hookTimeout: 30000
  //180000
};


```

<p>Add connection to your model file. </p>

```js

//config/models.js
module.exports.models = {


  connection: 'mysqlServer',


    //How and whether Sails will attempt to automatically rebuild the          
    //tables/collections/etc. in your schema.                                                                                                         
    //See http://sailsjs.org/#!/documentation/concepts/ORM/model-settings.html  

  migrate: 'alter'

};

```

<h2 class="section-heading">Setting Up Models</h2>

<p>We are going to use sails-cli to generate model </p>

```bash

   sails generate model School account_name:string city:string post_code:string edh_status:string edh_charity_id:string edh_url:string
```

<p>A new file will be created in <code>api/models/School.js</code></p>

```js
//models/School.js

 module.exports = {

  attributes: {

    account_name : { type: 'string' },

    city : { type: 'string' },

    post_code : { type: 'integer' },

    edh_status : { type: 'string' },

    edh_charity_id : { type: 'string' },

    edh_url : { type: 'string' },

    account: {model:'account',required:true,columnName:'account_id'}
  }
};

 ```



```js
 //api/models/Account.js

module.exports = {

  attributes: {

    email : { type: 'string',required:true,unique:true},

    password : { type: 'string',required:true }
  },
  toJSON: function () {
    var obj = this.toObject();
    delete  obj.password;
    delete obj.createdAt;
    delete obj.updatedAt;
  },
  checkPassword: function (password, user, cb) {
    require('machinepack-passwords').checkPassword({
      passwordAttempt: password,
      encryptedPassword: user.password
    }).exec({
      // An unexpected error occurred.
      error: function (err) {
        return cb(err, false);
      },
      // Password attempt does not match already-encrypted version
      incorrect: function () {
        return cb(null, false);
      },
      // OK.
      success: function () {
        return cb(null, true);
      }
    });
  }
};


 ```

 <p>This checkPassword method will compare the password. <code> npm install --save machinepack-passwords</code></p>

 <p> You can add relationship between models .Sails js using waterline ORM/ODM.Get more details about associations <a href="http://sailsjs.org/documentation/concepts/models-and-orm/associations">here</a></p>

<h2 class="section-heading">Defining Routes</h2>


<p>Basically,routes are rules that tell sails what to do when you
face incoming request</p>

```js

   // config/routes.js

   //School
  'POST /school':'SchoolController.create',
  'GET /school/:id':'SchoolController.findOne',

  //we use this route to perform login
  'POST /login' :'AuthController.login'

 ```

 <p>We did not create any action against routes. Create and Login are actions.Let us create actions in Controllers</p>

 <h2 class="section-heading">Setting Up Contrrollers</h2>

```js

 //controllers/SchoolController.js
"use strict";
module.exports ={

  create:function (req,res) {


    const validParams = ['email','password','account_name','city','post_code','edh_status',
     'edh_charity_id','edh_url'];
    const params = _.pick(req.body,validParams);



   let password = params.password,
       email= params.email,
       account_name=params.account_name,
       city= params.city,
       post_code= params.post_code,
       edh_charity_id= params.edh_charity_id,
       edh_url= params.edh_url,
       edh_status=params.edh_status;



    if (!password) {

      return res.badRequest({err:'Invalid password field'});
    }

    if (!email) {
      return res.badRequest({err:'Invalid email field'});
    }

    if (!(util.emailValidator.validate(email))) {
      return res.badRequest({err: 'Email is not valid'});
    }

    if(!account_name)
    {
      return res.badRequest({err:'Invalid account_name'});
    }

    if(!edh_charity_id)
    {
      return res.badRequest({err:'Invalid edh_charity_id'});
    }

   util.getEncryptedPassword(password, function(encPassword, err){

     if(!encPassword || err){
        res.forbidden({err: 'Your password is not matched'});
      }

    Account
      .create({email,password:encPassword})
      .then(account =>{

        if(!account) return res.negotiate({err:'Unable to create a new account'})

         return School
           .create({account_name,city,post_code,edh_charity_id,edh_status,edh_url,account:account.id});

      }).then(school =>{

      if(!school) return res.negotiate({err:'Unable to create a new account'});

      return res.json({msg:'Your account has been created successfully!'});

    }).catch(res.negotiate);
   });
  },

  //find a single school based on id
  findOne:function(req,res){

    let schoolId = req.params.id;

    School
    .findOne({id:schoolId})
    .then(res.ok)
    .catch(res.notFound);
  }

}

```

 <p>Run the sails app by  sails lift and go to this url <code> http://localhost:1337/school</code></p>

<a href="#">
    <img src="{{ site.baseurl }}/images/Signup.png" alt="Sample Signup Request">
</a>


 <h2 class="section-heading">Creating a Service</h2>

 <p><strong> Services</strong> are more like helpers that you can write once and use anywhere in your app. They are globalised by default, so you don’t need to require them.</p>

 <p>We are using jsonwebtoken npm package <code>npm install --save jsonwebtoken </code></p>

   ```js

//api/services/jsonwebtoken.js

var jwt = require('jsonwebtoken'),
    secret = 'KeEs84fF';

// Generates a token from supplied payload
module.exports.issue = function (payload, expiresIn) {
    if(!expiresIn)
        expiresIn = 10800; // in seconds
    return jwt.sign(
        payload,
        secret, // Token Secret that we sign it with
        {
            expiresIn: expiresIn // Token Expire time
        }
    );
};

// Verifies token on a request
module.exports.verify = function (token, callback) {
    return jwt.verify(
        token, // The token to be verified
        secret, // Same token we used to sign
        {}, // No Option, for more see https://github.com/auth0/node-jsonwebtoken#jwtverifytoken-secretorpublickey-options-callback
        callback //Pass errors or decoded token to callback
    );
};

  ```

 <h2 class="section-heading">Setting Up Policies</h2>



```js

//api/policies/isAuthorized.js

module.exports = function (req, res, next) {
  var token;

  if (req.headers && req.headers.authorization) {
    var parts = req.headers.authorization.split(' ');
    if (parts.length == 2) {
      var scheme = parts[0],
        credentials = parts[1];

      if (/^Bearer$/i.test(scheme)) {
        token = credentials;
      }
    } else {
      return res.json(401, {err: 'Format is Authorization: Bearer [token]'});
    }
  } else if (req.param('token')) {
    token = req.param('token');

    // We delete the token from param to not mess with blueprints
    //delete req.query.token; Enabled for demo purposes
  } else {
    return res.json(401, {err: 'No Authorization header was found'});
  }

  jwToken.verify(token, function (err, token) {
    if (err) {
      return res.json(401, {err: 'Invalid Token'});
    }

    School.findOne({id:token.school_id})
      .then(school =>{

        if(!school) return res.unauthorized({err:'No School found'});

        return Account
          .findOne({id:school.account})

      }).then(account => {

      if(!account) return res.unauthorized({err:'Invalid Token'});

      req.token = token;
      next();
    }).catch(res.unathorized);


  });
};


```

 <p>Get details about policies <a href="http://sailsjs.org/documentation/concepts/policies">here</a></p>

 <p> Let us test the login route. Run the Sails application by <code> sails-lift</code> </p>

 <a href="#">
    <img src="{{ site.baseurl }}/images/login.png" alt="Sample Signup Request">
</a>

<p> As an authenticated school and Teacher, He can be able to view his profile .We have to add policy for findOne route </p>


```js

 //config/policies.js

module.exports.policies = {

   //School
   SchoolController:{
   findOne:'isAuthorized'
   },
  AuthController :{
    login:true
  }

};

```

<p>We have received a token after loggedIn. We have to use this token to find school.</p>

 <a href="#">
    <img src="/images/findOne.png" alt="FindOne School">
</a>
<div style="text-align:center;">
<button class="btn btn-primary btn-lg" >
<a href="https://github.com/HaiderMalik12/sails-auth-app/tree/feature-signup-school" target="_blank">Code</a>
</button>
</div>

 <hr>

  {% include disqus.html %}
