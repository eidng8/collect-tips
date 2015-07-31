[TOC]


[GitHub]: http://github.com/ (GitHub Official Site)
[nodejs]: http://nodejs.org/ (nodejs Official Site)
[grunt]: http://gruntjs.com/ (Grunt Official Site)

## [Node.js][nodejs]

No need to explain, every front-end guy knows it, some back-end guys also know it.

As it's outside Chain mainland, accessing is difficult. [Mirror](http://npm.taobao.org/) can be used. There's descriptions on the site, `cnpm` is suggested.

```bash
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

Then `cnpm` can be used instead of `npm`.

`cnpm` seems gooed enough, but it creates its own cache, so I've switched back to `npm`:

```bash
npm config -g set registry https://registry.npm.taobao.org
```


## [Grunt][grunt]

[Grunt][grunt] is a task runner on [Node.js][nodejs], just like Apache Ant.

- Ater [Node.js][nodejs] and [GitHub client][github] have been installed, find the `git shell` in Windows Start menu and run it to popup the command prompt.
- In `Git Shell` prompt
  ```bash
  npm install -g grunt-cli
  ```
