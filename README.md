# React Atlas
React Atlas is a React component library, with a focus on supplying Admin Interface tools. The goal of this repo to is to eventually be the library that can power most of Digital River's complex admin interfaces. With this in mind, we need a fast, generic, composable library that can be dropped into a project and 'just work'.

## Why?
React Atlas originally started off as a fork of [React Toolbox](https://github.com/react-toolbox/react-toolbox). We liked the hierarchy and the way the components were built. However, we didn't want to be married to the Material Design concept, and wanted to make a library that was a little more generic. We hope that React Atlas will be that tool.

## Requirements
If using this Library via NPM, you will need to make sure you reference the CSS file that is packaged with it. That should be it. Oh, also this library only officially supports [Node 4.2.x](https://nodejs.org/en/).

If you wish to use this project via a fork, and build/minifiy on your own, you will need to account for the following:

This project uses CSS Modules and CSS Next for styling. To process this we use PostCSS. ([Read why here](https://github.digitalriverws.net/ux/react-atlas/wiki/Decisions#a-note-on-css)). At minimum your application will need to have the following packages to correctly interpret and use our library:
- [PostCSS](https://github.com/postcss/postcss), with the following plugins:
  - [PostCSS Import](https://github.com/postcss/postcss-import)
  - [CSS Next](https://github.com/cssnext/postcss-cssnext)
- A way to interpret CSS Modules, could be any of the following depending on your environment:
  - [Webpack CSS Loader](https://github.com/webpack/css-loader)
  - [PostCSS Modules](https://github.com/outpunk/postcss-modules)
  - [CSS Modules Require Hook](https://github.com/css-modules/css-modules-require-hook)

## Usage

For inital development and release, we are focusing on a nodejs with webpack environment. As we continue to develop React Atlas we will bring in examples and boilerplates to show it working with other build systems (JSPM, Browserify, UMD, etc.).

With webpack in mind, we reccomend using [Babel Loader](https://github.com/babel/babel-loader), [CSS Loader](https://github.com/webpack/css-loader), [PostCSS Loader](https://github.com/postcss/postcss-loader) and [SASS Loader](https://github.com/jtangelder/sass-loader) (for now, SASS will be removed from this project soon. We are working toward dropping the Sass and Webpack dependency as soon as it makes sense for us internally. A good starting point is for a webpack workflow is [React Hot Webpack Boilerplate](https://github.com/gaearon/react-hot-boilerplate).

Requiring and using the components is as simple as:

```jsx
import React from 'react';
import {Button} from 'react-atlas';

const someButton = () => (
  <Button label="Some Text" />
);

export default someButton;
```

The previous code creates a React button component based on a React Atlas button. It's important to notice that requiring a module from the exposed root of the package will import the **SASS** of the component. We are working to change this as soon as possible, and hope to get away from SASS to help enable this library to be environment agnostic.

## Customization

Since React Atlas styles are written in CSS it's pretty easy to customize your components:

### Via `className` property

Generally each component will have a `className` prop so you can tell the class name you want to keep in the root node of the resulting markup. All markup is style with the lowest specificity level so you can just nest one level in your CSS and the result will be applied. Consider this example:

```jsx
const CustomButton = () => (
  <Button className='customized' label='Custom button' />
);
```

If you browse the resulting markup you will see *data attributes* like `data-role="label"` so you can avoid styling directly tag names. You can now write your CSS:

```css
.customized > [data-role="label"] {
  color: green;
  font-weight: bold;
}
```

We will be thinking hard about styling going forward and this workflow may change. We want to make overriding the React Atlas styles as simple as possible. Something like [React Themeable](https://github.com/markdalgleish/react-themeable) may be used.

## Local Docs

To work in the project you'd need a `node` version supporting ES6 syntax. Although the project is built using Babel we use some ES6 features in the development server. Also, the packages has been tested with `node 4.2.1`. Consider using [nvm](https://github.com/creationix/nvm) or [n](https://github.com/tj/n) to handle different node versions!

To start documentation site locally you'd need to install dependencies from the main package and also dependencies from the docs subproject:

```
git clone https://github.com/react-toolbox/react-toolbox.git
npm install
cd docs/
npm install 
npm start
```

Local documentation will be available at http://localhost:3001/

## Authors and Contributors
Before cloning or submitting a Pull Request, ***please read our [Contributing Guidelines](https://github.digitalriverws.net/ux/react-atlas/blob/master/CONTRIBUTING.md)***

The project is being initially developed and maintained by the DR UX team.

## [Read the Wiki](https://github.digitalriverws.net/ux/react-atlas/wiki)
Check out [our wiki](https://github.digitalriverws.net/ux/react-atlas/wiki) for more information on coding conventions, why we made certain decisions and a roadmap.

## Set-Up/Installation for Development and Contributing

### Windows Users
If running on windows, Follow these steps to ensure you don't run into any 'node-gyp' issues:

[Install VC++ Build Tools Technical Preview](https://www.microsoft.com/en-us/download/confirmation.aspx?id=49983)

>:bulb: [Windows 7 only] requires [.NET Framework 4.5.1](http://www.microsoft.com/en-us/download/details.aspx?id=40773)

[Install Python 2.7](https://www.python.org/downloads/), and add it to your PATH, ```npm config set python python2.7```

Launch cmd, ```npm config set msvs_version 2015``` --global 

### Clone and Start Spec/Style Guide Page
The following commands will clone the repo down, install npm dependencies and start the specs/style guide page.
```
git clone git@github.digitalriverws.net:ux/react-atlas.git
cd react-atlas
npm install
cd docs/
npm install 
cd ..
npm run start
```
Spec page will be at ```http://localhost:3001/```

## License 
This project is licensed under the terms of the [MIT license](https://github.com/react-toolbox/react-toolbox/blob/master/LICENSE).

## Atlas?
When thinking about Web Design and Web Development, we came across the art of map making - [Cartography](https://en.wikipedia.org/wiki/Cartography).

>Cartography (from Greek χάρτης khartēs, "map"; and γράφειν graphein, "write") is the study and practice of making maps. Combining science, aesthetics, and technique, cartography builds on the premise that reality can be modeled in ways that communicate spatial information effectively.

After reading about it more, we realized that as Web Designer and Developers, we are essentially modern-day map makers. We combine technology and design to build flat screens that communicate information in a fixed space. With this reasoning in our heads, we decided on Atlas. Atlas is defined as a collection(or a _library_ if you will) of maps. What better name for a library of components that will be used to compose and display complex interfaces/maps?

Plus you know, there's this cool Titan in Greek mythology that literally holds up the world named Atlas.
