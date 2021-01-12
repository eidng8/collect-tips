[TOC]


[GitHub]: http://github.com/ (GitHub Official Site)
[nodejs]: http://nodejs.org/ (nodejs Official Site)
[grunt]: http://gruntjs.com/ (Grunt Official Site)
[angular]: https://angularjs.org/ (AngularJS Official Site)
[ionic]: http://ionicframework.com/ (Ionic Official Site)
[cordova]: https://cordova.apache.org/ (Apache Cordova Official Site)


## [Node.js][nodejs]

### `cnpm`

No need to explain, every front-end guy knows it, some back-end guys also know it.

As it's outside China mainland, accessing is difficult. [Mirror](http://npm.taobao.org/) can be used. There's descriptions on the site, `cnpm` is suggested.

```bash
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

Then `cnpm` can be used instead of `npm`.

`cnpm` seems gooed enough, but it creates its own cache, so I've switched back to `npm`:

```bash
npm config -g set registry https://registry.npm.taobao.org
```

### `mirror-config-china`

Instead of using the `cnpm` pacakge, one could install the `mirror-config-china` package to directly change all related stuff to China mirror.


## [Grunt][grunt]

[Grunt][grunt] is a task runner on [Node.js][nodejs], just like Apache Ant.

- Ater [Node.js][nodejs] and [GitHub client][github] have been installed, find the `git shell` in Windows Start menu and run it to popup the command prompt.
- In `Git Shell` prompt
  ```bash
  npm install -g grunt-cli
  ```


## [AngularJS][angular]

Single page application framework on JavaScript. It's not a DOM manipulator, nor a designer's tool or trade. [AngularJS][angular] introduced the way of building applications right at the page that users see in browsers.


### Tutorials

#### Online

##### Official

https://docs.angularjs.org/tutorial/

##### 3rd Parties
http://www.w3schools.com/angular/
http://www.toptal.com/angular-js/a-step-by-step-guide-to-your-first-angularjs-app
https://www.codecademy.com/courses/learn-angularjs
https://thinkster.io/a-better-way-to-learn-angularjs/
http://www.tutorialspoint.com/angularjs/


#### PDF

http://www.tutorialspoint.com/angularjs/angularjs_tutorial.pdf
http://fastandfluid.com/publicdownloads/AngularJSIn60MinutesIsh_DanWahlin_May2013.pdf


## [Ionic][ionic]

Cross-platform mobile application framework, also compatible with desktop application development. Base on [AngularJS][angular] & [Cordova][cordova].


### Tutorials

#### Online

##### Official

http://learn.ionicframework.com/

##### 3rd Parties

https://ccoenraets.github.io/ionic-tutorial/
https://thinkster.io/ionic-framework-tutorial/
http://coenraets.org/blog/2014/10/ionic-tutorial-and-sample-application/
https://www.airpair.com/ionic-framework/posts/ionic-socketio-chat-application-tutorial


#### PDF

https://ma.ellak.gr/documents/2014/10/ionic-framework.pdf
http://manning.com/wilken/IonicinA_MEAP_ch01.pdf


## [Nightwatch](https://nightwatchjs.org/)

Working with sections and custom command/assert are tricky. [issue](https://github.com/nightwatchjs/nightwatch/issues/1969)

