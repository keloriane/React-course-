To work in React, we will need a working environment mainly based on Node js. If it is not already installed




Creates a working folder for React in which all projects are placed.
Install and create your React project with the terminal.
Finally, use the "create-react-app" command in global. This command is there to create the skeleton of our application, we could very well do it by hand but it's a waste of time.



``
npm install -g create-react-app
``

Once the package is installed, create a folder where you want to store your app and type the command :

``
create-react-app todo
``

Normally our application has been generated, so we will start it.

``
cd series
npm start
``

After launching the "npm start" command, your application will be available at the following address: localhost:3000. She sets up a livereloading system so that each time you save a file, the app updates itself without having to reload the page.

To test, modify the "Welcome To React" line in App.js with another title and then check in the browser that all this changes automatically without refresh.

