+++
date = "2015-01-03T09:34:15+01:00"
title = "Auth Fails error when connecting to Mongo"
tags = ["MongoDb", "MongoLab"]
menu = ""
banner = "banners/mongodb.jpg"


+++

I've been playing around with MongoDb a bit recently,  using the free tier of the MongoLab service on Azure.

Connecting to Mongolab via terminal using the below command ;

    `mongo xxxxxx.mongolab.com:xxxxx/DBName -u <username> -p <password>`

came back with the following error.

    MongoDB shell version: 2.6.0
    connecting to: xxxxxx.mongolab.com:xxxxx/DBname
    2014-09-24T23:01:18.984+0100 Error: 18 { code: 18, ok: 0.0, errmsg: "auth fails" } at src/mongo/shell/db.js:1210
    exception: login failed

I repeated the process, and the same happened again. The credentials were absolutely correct, as was the connection string.

Fortunately Mongolabs' support is quick, and by quick, i mean *super-quick*. Less than 5 minutes after i'd emailed them they got back to me with some diagnostic information

   Wed Sep 24 15:01:17.960 [initandlisten] connection accepted from 86.153.168.248:62035 #463878 (268 connections now open)

    Wed Sep 24 15:01:18.275 [conn463878]  authenticate db: DBName { authenticate: 1, nonce: "4e36d04ecd3376d1", user: "MyUserName", key: "655f7054037b5188c385fd94605f84cf" }

    Wed Sep 24 15:01:18.275 [conn463878] auth: key mismatch MyUserName, ns:DBName

It turns out that the password was incorrect, because i'd got characters in the password that needed escaping.

So using a password with nothing esoteric character-wise is probably a safe option to avoid errors like this in the future. 





