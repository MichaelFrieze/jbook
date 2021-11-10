## Quick Notes

> `npm audit` says there is a vulnerability in react-scripts.

[Link to Dan Abramov talking about this in CRA](https://github.com/facebook/create-react-app/issues/11174)

```
npm audit says there's a warning about vulnerabilities in my project
Open package.json. You will find this:

  "dependencies": {
    "react": "^17.0.2",
    "react-dom": "^17.0.2",
    "react-scripts": "4.0.3"
  }
Take react-scripts and move it to devDependencies (if you don't have it, create it):

  "dependencies": {
    "react": "^17.0.2",
    "react-dom": "^17.0.2"
  },
  "devDependencies": {
    "react-scripts": "4.0.3"
  },
Then, ensure you run npm audit --production rather than npm audit.

This will fix your warnings.

But isn't this just ignoring the problem?
No.

Create React App is a build tool. In other words, it doesn't produce a running Node application. It runs at the build time during development, and produces static assets.

However, npm audit is designed for Node apps so it flags issues that can occur when you run actual Node code in production. That is categorically not how Create React App works.

This means that the overwhelming amount of "vulnerability" reports we receive for transitive dependencies are false positives. Despite literally a hundred issues with thousands of comments about npm audit warnings in react-scripts, throughout the years not a single one of them (to the best of our knowledge) has ever been a real vulnerability for CRA users.

This is a huge waste of everyone's time. Mostly of yours, but of ours too.

But I still see these warnings when creating a new project or running npm install
Yes, unfortunately that's how npm works since v6. You can bring it up with npm. If enough people complain, maybe they'll rethink this decision. It is unfortunately actively hostile to build tooling.

Note that you can run npm install --no-audit to suppress them.
```
