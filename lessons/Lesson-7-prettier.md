---
path: "/prettier"
title: "Prettier"
order: "7A"
description: "An opinionated code formatter; Supports many languages; Integrates with most editors;"
section: "JS Tools"
---

[](#code-quality)Code Quality
-----------------------------

It's important to keep quality high when writing code. Or at least that's how I sell ESLint and Prettier to my
co-workers. In reality, I'm super lazy and want the machine to do as much work as possible so I can focus more on
architecture and problem-solving and less on syntax and style. While there are many tools that can help you keep code
quality high, these two I consider core to my workflow.

[Prettier](https://github.com/prettier/prettier) is an amazing tool from the brain
of [James Long](https://twitter.com/jlongster). James, like many of us, was sick of having to constantly worry about the
style of his code: where to stick indents, how many, when to break lines, etc etc. Coming from languages like Go,
Reason, or Elm where all that is just taken care of by the tooling for the language, this quickly wears. James did
something about it and made a tool to take care of it: Prettier.

Prettier is a really fancy pretty printer. It takes the code you write, breaks it down in to an abstract syntax tree (
AST) which is just a representation of your code. It then takes that AST, throws away all of your code style you made
and prints it back out using a predefined style. While this sounds a little scary, it's actually really cool. Since you
no longer have control of the style of your code, you no longer have to think about it at all. Your code is always
consistent, as is the code from the rest of your team. No more bikeshedding!! As I like to put it: if your brain is a
processor, you get to free up the thread of your brain that worries about code styles and readability: it just happens
for you. Don't like semicolons? Don't write them! It puts them in for you. I _love_ Prettier.

Need to tool around a bit with it before you trust it? [Go here](https://prettier.io/playground/). You can see how it
works.

Let's go integrate this into our project. It's _pretty_ easy (lol.)

Either install Prettier globally `npm install --global prettier` or replace when I run `prettier` with (from the root of
your project) `npx prettier`. From there, run `prettier script.js`. This will output the formatted version of your file.
If you want to actually write the file, run `prettier --write script.js`. Go check script.js and see it has been
reformatted a bit. I will say for non-JSX React, prettier makes your code less readable. Luckily Prettier supports JSX!
We'll get to that shortly.

Prettier has a few configurations but it's mostly meant to be a tool everyone uses and doesn't argue/bikeshed about the
various code style rules. [Here they are](https://prettier.io/docs/en/options.html). I just use it as is since I'm lazy.
Prettier can also understand [flow](https://flow.org/) and [TypeScript](https://www.typescriptlang.org/).

Prettier is great to use with [Visual Studio Code](https://code.visualstudio.com/?WT.mc_id=reactintro-github-brholt).
Just
download [this extension](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode&WT.mc_id=reactintro-github-brholt)
. Pro tip: set it to only run Prettier when it detects a Prettier config file. Makes it so you never have to turn it
off. In order to do that, set `prettier.requireConfig` to `true` and `editor.formatOnSave` to true.

So that our tool can know this is a Prettier project, we're going to create a file called `.prettierrc` and put 
```json
{}
```
in it. This lets everyone know this is a Prettier project that uses the default configuration. You can put other configs
here if you hold strong formatting opinions. **for example here's mine** 
```json
{
  "singleQuote": true,
  "printWidth": 100,
  "proseWrap": "always",
  "trailingComma": "none",
  "bracketSpacing": true,
  "jsxBracketSameLine": false,
  "semi": false
}
```

[](#npmyarn-scripts)npm/Yarn scripts
------------------------------------

So it can be painful to try to remember the various CLI commands to run on your project. You can put CLI commands into
it and then run the name of the tag and it'll run that script. Let's go see how that works. Put the following into your
package.json.

First run `npm install -D prettier`. `-D` means it's for development only.
```json
{
  "scripts": {
    "format": "prettier --write \"src/**/*.{js,jsx}\""
  }
}
```
Now you can run `yarn format` or `npm run format` and it will run that command. This means we don't have to remember
that mess of a command and just have to remember format. Nice, right? We'll be leaning on this a lot during this course.

[](#alternatives)Alternatives
-----------------------------

There really aren't any for Prettier. The alternative is just not to use a formatter. ESLint's `--fix` flag would be the
closest thing.

> 🏁 [Click here to see the state of the project up until now - Prettier](https://github.com/mohammedelzanaty/react-guide-with-zanaty/commit/fab751364db44631d96b4af16fab3a202589d432)
