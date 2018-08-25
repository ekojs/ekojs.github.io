---
id: 161
title: Integrate Extjs4.2 with NodeJS
date: 2016-03-04T07:30:07+00:00
author: Eko Junaidi Salam
layout: post
guid: http://ekojunaidisalam.com/?p=161
permalink: /2016/03/04/integrate-extjs4-2-with-nodejs/
dsq_thread_id:
  - "4632217628"
categories:
  - Artikel
  - Programming
  - Teknologi
  - 'Tip &amp; Trik'
tags:
  - extjs
  - framework
  - integrate
  - javascript
  - nodejs
  - web desktop
---
<h2 style="text-align: center;">
  <a href="{{site.baseurl}}/wp-content/uploads/2016/02/web-desktop.png" rel="attachment wp-att-162"><img class="aligncenter wp-image-162 size-large" src="{{site.baseurl}}/wp-content/uploads/2016/02/web-desktop-1024x576.png" alt="Integrate" width="584" height="329" srcset="{{site.baseurl}}/wp-content/uploads/2016/02/web-desktop-1024x576.png 1024w, {{site.baseurl}}/wp-content/uploads/2016/02/web-desktop-300x169.png 300w, {{site.baseurl}}/wp-content/uploads/2016/02/web-desktop-768x432.png 768w, {{site.baseurl}}/wp-content/uploads/2016/02/web-desktop-500x281.png 500w, {{site.baseurl}}/wp-content/uploads/2016/02/web-desktop.png 1366w" sizes="(max-width: 584px) 100vw, 584px" /></a><br /> Integrate ExtJS4.2 and NodeJS &#8211; Web Desktop Examples
</h2>

To integrate Extjs4.2 and NodeJS, we need to know how this works before. If you build ExtJS using <a href="http://docs.sencha.com/extjs/4.2.2/#!/guide/command" target="_blank">Sencha Cmd</a>, then you&#8217;re in the right path. You need to initialize your node package using `npm init`, to list everything we need in `package.json`. And then, create your app using `sencha generate app` command.<a name='more'></a>

Alright, let&#8217;s follow this command below how to do that. I assume you have installed Sencha Cmd v4.0.5.87 and NodeJS v4.2.2 or the latest stable version Correctly with NPM v2.14.7 installed. Check the version `sencha` for Extjs, `node -v` for NodeJS, `npm -v` for Node Package Manager. Here&#8217;s how to integrate ExtJS and NodeJS :

  1. mkdir web-desktop for creating new folder in your working directory.
  2. npm init for creating package.json to store information for your project version, dependencies, and other related information about your project.
  3. Install node package express and other package you need.
  4. After that, generate app for the secha app template.
  5. And the last, create your index.js file and run it.

**Here&#8217;s Example code&#8230;**
  
For complete Example Web-Desktop Source Code from sencha please fork/download in <a href="https://github.com/ekojs/Web-Desktop" target="_blank">Github</a>. Untuk hasil dari renderingnya bisa dicek di <a href="https://ekojs.github.io/Web-Desktop/" target="_blank">https://ekojs.github.io/Web-Desktop/</a>

npm init
  
<code>PS C:\xampp\htdocs\web-desktop> cat .\package.json<br />
{<br />
"name": "web-desktop",<br />
"version": "1.0.0",<br />
"description": "Web Desktop, Integrate Extjs4.2 and NodeJS",<br />
"main": "index.js",<br />
"dependencies": {<br />
"express": "^4.13.4"<br />
},<br />
"devDependencies": {},<br />
"scripts": {<br />
"test": "echo \"Error: no test specified\" && exit 1"<br />
},<br />
"keywords": [<br />
"web",<br />
"desktop",<br />
"ExtJS",<br />
"NodeJS"<br />
],<br />
"author": "ekojs",<br />
"license": "ISC"<br />
}
</code>

npm install
  
<code>PS C:\xampp\htdocs\web-desktop> npm install express --save<br />
express@4.13.4 node_modules\express<br />
├── escape-html@1.0.3<br />
├── array-flatten@1.1.1<br />
├── fresh@0.3.0<br />
├── cookie-signature@1.0.6<br />
├── range-parser@1.0.3<br />
├── cookie@0.1.5<br />
├── serve-static@1.10.2<br />
├── content-type@1.0.1<br />
├── parseurl@1.3.1<br />
├── content-disposition@0.5.1<br />
├── utils-merge@1.0.0<br />
├── etag@1.7.0<br />
├── methods@1.1.2<br />
├── path-to-regexp@0.1.7<br />
├── merge-descriptors@1.0.1<br />
├── vary@1.0.1<br />
├── depd@1.1.0<br />
├── qs@4.0.0<br />
├── finalhandler@0.4.1 (unpipe@1.0.0)<br />
├── on-finished@2.3.0 (ee-first@1.1.1)<br />
├── proxy-addr@1.0.10 (forwarded@0.1.0, ipaddr.js@1.0.5)<br />
├── debug@2.2.0 (ms@0.7.1)<br />
├── type-is@1.6.11 (media-typer@0.3.0, mime-types@2.1.9)<br />
├── accepts@1.2.13 (negotiator@0.5.3, mime-types@2.1.9)<br />
└── send@0.13.1 (statuses@1.2.1, ms@0.7.1, destroy@1.0.4, mime@1.3.4, http-errors@1.3.1)<br />
PS C:\xampp\htdocs\web-desktop> npm ls --depth=0<br />
C:\xampp\htdocs\web-desktop<br />
└── express@4.13.4<br />
PS C:\xampp\htdocs\web-desktop>
</code>

sencha generate app
  
<code>PS C:\xampp\htdocs\web-desktop> sencha -sdk ..\extjs-4.2\ generate app EJS .<br />
Sencha Cmd v4.0.5.87<br />
[INF]<br />
[INF] init-plugin:<br />
[INF]<br />
[INF] -before-generate-workspace:<br />
[INF]<br />
[INF] cmd-root-plugin.init-properties:<br />
[INF]<br />
[INF] init-properties:<br />
[INF]<br />
[INF] init-sencha-command:<br />
[INF]<br />
[INF] init:<br />
[INF]<br />
[INF] generate-workspace-impl:<br />
[INF] [echo] generating into C:\xampp\htdocs\web-desktop\. from C:\Sencha\Cmd\4.0.5.87/templates/workspace<br />
[INF] [mkdir] Created dir: C:\xampp\htdocs\web-desktop\packages<br />
[INF]<br />
[INF] cmd-root-plugin.copy-framework-to-workspace-impl:<br />
[INF] [propertyfile] Updating property file: C:\xampp\htdocs\web-desktop\.sencha\workspace\sencha.cfg<br />
[INF]<br />
[INF] copy-framework-to-workspace-impl:<br />
[INF] [copy] Copying 4884 files to C:\xampp\htdocs\web-desktop\ext<br />
[INF] [copy] Copying 89 files to C:\xampp\htdocs\web-desktop\ext\src\ux<br />
[INF] [propertyfile] Updating property file: C:\xampp\htdocs\web-desktop\.sencha\workspace\sencha.cfg<br />
[INF]<br />
[INF] copy-framework-to-workspace:<br />
[INF]<br />
[INF] generate-workspace:<br />
[INF]<br />
[INF] -after-generate-workspace:<br />
[INF]<br />
[INF] init-plugin:<br />
[INF]<br />
[INF] cmd-root-plugin.init-properties:<br />
[INF]<br />
[INF] init-properties:<br />
[INF]<br />
[INF] init-sencha-command:<br />
[INF]<br />
[INF] init:<br />
[INF]<br />
[INF] before-upgrade:<br />
[INF]<br />
[INF] generate-app-impl:<br />
[INF]<br />
[INF] generate-starter-app:<br />
[INF] [mkdir] Created dir: C:\xampp\htdocs\web-desktop\resources<br />
[INF] [mkdir] Created dir: C:\xampp\htdocs\web-desktop\overrides<br />
[INF] [mkdir] Created dir: C:\xampp\htdocs\web-desktop\sass\src<br />
[INF] [mkdir] Created dir: C:\xampp\htdocs\web-desktop\sass\var<br />
[INF] [mkdir] Created dir: C:\xampp\htdocs\web-desktop\sass\etc<br />
[INF] [x-property-file] Updating property file: C:\xampp\htdocs\web-desktop\.sencha\app\sencha.cfg<br />
[INF]<br />
[INF] after-upgrade:<br />
[INF]<br />
[INF] init-plugin:<br />
[INF]<br />
[INF] cmd-root-plugin.init-properties:<br />
[INF]<br />
[INF] init-properties:<br />
[INF]<br />
[INF] init-sencha-command:<br />
[INF]<br />
[INF] init:<br />
[INF]<br />
[INF] app-refresh:<br />
[INF] [echo] Refreshing app at C:\xampp\htdocs\web-desktop<br />
[INF]<br />
[INF] app-refresh-impl:<br />
[INF]<br />
[INF] -before-init-local:<br />
[INF]<br />
[INF] -init-local:<br />
[INF]<br />
[INF] -after-init-local:<br />
[INF]<br />
[INF] init-local:<br />
[INF]<br />
[INF] find-cmd-in-path:<br />
[INF]<br />
[INF] find-cmd-in-environment:<br />
[INF]<br />
[INF] find-cmd-in-shell:<br />
[INF]<br />
[INF] init-cmd:<br />
[INF] [echo] Using Sencha Cmd from C:\Sencha\Cmd\4.0.5.87 for C:\xampp\htdocs\web-desktop\build.xml<br />
[INF]<br />
[INF] -before-init:<br />
[INF]<br />
[INF] -init:<br />
[INF] Initializing Sencha Cmd ant environment<br />
[INF] Adding antlib taskdef for com/sencha/command/compass/ant/antlib.xml<br />
[INF]<br />
[INF] -after-init:<br />
[INF]<br />
[INF] -before-init-defaults:<br />
[INF]<br />
[INF] -init-defaults:<br />
[INF]<br />
[INF] -after-init-defaults:<br />
[INF]<br />
[INF] -init-compiler:<br />
[INF]<br />
[INF] init:<br />
[INF]<br />
[INF] refresh:<br />
[INF]<br />
[INF] -before-refresh:<br />
[INF]<br />
[INF] -init:<br />
[INF]<br />
[INF] -init-compiler:<br />
[INF]<br />
[INF] -detect-app-build-properties:<br />
[INF] Loading app json manifest...<br />
[INF] Loading classpath entry C:\xampp\htdocs\web-desktop\ext\src<br />
[INF] Loading classpath entry C:\xampp\htdocs\web-desktop\ext\packages\ext-theme-base\src<br />
[INF] Loading classpath entry C:\xampp\htdocs\web-desktop\ext\packages\ext-theme-base\overrides<br />
[INF] Loading classpath entry C:\xampp\htdocs\web-desktop\ext\packages\ext-theme-neutral\src<br />
[INF] Loading classpath entry C:\xampp\htdocs\web-desktop\ext\packages\ext-theme-neutral\overrides<br />
[INF] Loading classpath entry C:\xampp\htdocs\web-desktop\ext\packages\ext-theme-classic\src<br />
[INF] Loading classpath entry C:\xampp\htdocs\web-desktop\ext\packages\ext-theme-classic\overrides<br />
[INF] Loading classpath entry C:\xampp\htdocs\web-desktop\app<br />
[INF] Loading classpath entry C:\xampp\htdocs\web-desktop\app.js<br />
[INF] Loading classpath entry C:\xampp\htdocs\web-desktop\build\temp\production\EJS\sencha-compiler\app<br />
[INF] Loading classpath entry C:\xampp\htdocs\web-desktop\build\temp\production\EJS\sencha-compiler\app<br />
[INF] Concatenating output to file C:\xampp\htdocs\web-desktop/build/temp/production/EJS/sencha-compiler/cmd-packages.js<br />
[INF] Adding external reference : @full-page => @overrides<br />
[INF] Loading classpath entry C:\xampp\htdocs\web-desktop\build\temp\production\EJS\sencha-compiler\cmd-packages.js<br />
[INF] Adding external reference : Ext.util.Observable => C:\xampp\htdocs\web-desktop/build/temp/production/EJS/sencha-compiler/cmd-packages.js<br />
[INF]<br />
[INF] -refresh-app:<br />
[INF] Appending concatenated output to file C:\xampp\htdocs\web-desktop/bootstrap.js<br />
[INF] Appending concatenated output to file C:\xampp\htdocs\web-desktop/bootstrap.js<br />
[INF] Appending concatenated output to file C:\xampp\htdocs\web-desktop/bootstrap.js<br />
[INF] Appending concatenated output to file C:\xampp\htdocs\web-desktop/bootstrap.js<br />
[INF] Appending concatenated output to file C:\xampp\htdocs\web-desktop/bootstrap.js<br />
[INF] Appending content to C:\xampp\htdocs\web-desktop/bootstrap.js<br />
[INF] Appending content to C:\xampp\htdocs\web-desktop/bootstrap.json<br />
[INF]<br />
[INF] -refresh:<br />
[INF]<br />
[INF] -after-refresh:<br />
[INF]<br />
[INF] after-upgrade:<br />
[INF]<br />
[INF] generate-app:<br />
[INF]<br />
[INF] -after-generate-app:<br />
[INF] [x-property-file] Updating property file: C:\xampp\htdocs\web-desktop\.sencha\app\sencha.cfg<br />
PS C:\xampp\htdocs\web-desktop>
</code>

File index.js for nodejs
  
<code>var express = require("express");<br />
var fs = require("fs");<br />
var app = express();<br />
app.use('/resources',express.static('resources'));<br />
app.use('/app',express.static('app'));<br />
app.use('/ext',express.static('ext'));<br />
app.use('/sass',express.static('sass'));<br />
app.use('/app.js',express.static(__dirname + '/app.js'));<br />
app.use('/app.json',express.static(__dirname + '/app.json'));<br />
app.use('/bootstrap.js',express.static(__dirname + '/bootstrap.js'));<br />
app.use('/bootstrap.json',express.static(__dirname + '/bootstrap.json'));<br />
app.use('/bootstrap.css',express.static(__dirname + '/bootstrap.css'));<br />
app.get("/",function(req,res){<br />
res.sendFile(__dirname+"/"+"index.html");<br />
});<br />
var server = app.listen(8088,function(){<br />
var host = server.address().address;<br />
var port = server.address().port;<br />
console.log("App Listening at http://%s:%s Created by Eko Junaidi Salam",host,port);<br />
})
</code>
