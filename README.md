# Creating Your Own npm Package using TypeScript

## Step 1: Create the Project

First, create the project by running the following commands in your terminal or command prompt.

```bash
mkdir my-first-npm
cd my-first-npm
```

Now you are in the project folder. Next, open your favorite IDE. In this example, I am using VS Code. To open VS Code from this location, use the following command:

```bash
code .
```

To initialize the node.js project use,

```bash
npm init -y
tsc --init
```

It will create package.json and tsconfig.json files in your project location. Then install the dependencies of the project. we just need del-cli and typescript.

```bash
npm i del-cli typescript
```

Then create a src folder and create two files called index.ts. and example.ts. Then write this small code. I think everyone can identify these two small commands.

![npm-package](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*F8cclSjTjndcRbkxXnOFqw.png)


```typescript
// index.ts
const doubleYourAge = (age: number) => {
return age * 2;
};
export { doubleYourAge };
```

Then exmaple.ts

```typescript
// exmaple.ts
export * from './example'
```


What we simply going to create is a package double your age. I know this is useless but for example, it is good.

Now we have to do some configurations and then publish the npm to npmjs.com.

Then move to tsconfig.json do the following changes.

```bash
# comment out “declaration”: true for declaring the types for typescripts. 
# comment out “outDir”: “./build” and give it location as “./build” to output the javascript version of our code in the folder called build.
```


Then the tsconfig.json files configuration is over. Then move to the package.json file.

Then write two scripts in the package.json file like below.


```bash
"clean":"del ./build/*",
"build":"npm run clean && tsc"
```


And run,

```bash
npm run build
```

Every time when you run npm run build “clean”: “del ./build” will clear the build folder.

Then you can see the build folder is created and it has the js and type definition files.

After that in the package.json file do these changes.


```bash
"main": "./build/index.js",
"types": "./build/index.d.ts",
"files": ["build/**/*"],
```

This command basically indicates that index.js is the main file of the project and its type definition.

Now all the configuration has been done and then we have to create our account in npmjs.com. for that go to npmjs.com and signup and verify your email. All of these things are free.

Then click the profile button (rounded button) and click add organization. Then provide a unique name. I provide the name as exmaplefirst. Then click the Unlimited public packages create button and click the skip button.

Ohh yes, now you create your organization.

Then change the name of your project in the package.json file to @<your_npm_organization_name>/any_name_you_like for_your_project.

In my case, it is like this. “name”: “@exmaplefirst/my-first-npm”,

Now go to the code and create a git repo and add a .gitignore file. To create a git repo use the below command,


```bash
git init
```

Add node_modules and build folder to the .gitignore. Then add your files to the git repo.

```bash
git add .
git commit -m "initial commit"
```

Then run npm login and provide the required data to log to the npm.

```bash
npm login
```


Then run,

```bash
npm publish --access public
```

yes. Now you publish your first npm library to the npmjs and you can see it from your profile in npmjs. I can see it in my account as @exmaplefirst/my-first-npm.

Then we can check that package. For that I quickly create a node.js project with express and install that library and check if it work.


```bash
mkdir check
cd check
npm init -y
npm install express nodemon @exmaplefirst/my-first-npm
```

write start script in package.json as “start”:”nodemon index.js”. Then create an index.js file and write small code to check the package.



```typescript
const express = require("express");
const app = express();
const { doubleYourAge } = require("@exmaplefirst/my-first-npm");
app.use(express.json());
app.get("/api", (req, res) => {
const age = 20;
const dAge = doubleYourAge(age);
return res.status(200).send({ age: dAge });
});
app.listen(3005, () => {
console.log("server start on port 3005");
});
```


Then start the terminal and run the command npm start.

Then start your browser and navigate to localhost:3005/api.

you can see the output as {age:”40”}.

Yes, it is the end. Know you know how to create your own npm package, how can you publish it to npmjs, and how to check it.




