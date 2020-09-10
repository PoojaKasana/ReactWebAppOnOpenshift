# ReactWebAppOnOpenshift

Hosting React web app on Openshift platform 
We are trying to host the project ABC's designed storybook web app on Openshift platform using node js server and react app(can be any web app) as static content. 


Project Setup 

•	Need to have the below folder structure where in root folder there will be a package.json and index.js/ server.js file.  express js will be imported and configured in this server.js file. 

          ABCdesignSystem/
                ├── server.js/
                ├── package.json/
                ├── client
                      ├── package.json
                      └── src
                      └── storybook

•	Add below in server.js/index.js to setup the server.  Here storybook-static will be the output of storybook build which can be served/hosted on any server 

index.js/server.js 

const app = express(); 

app.use(express.static(path.join(__dirname, ‘client/storybook-static'))); 

app.get('/*', function(req, res) { 

  res.sendFile(path.join(__dirname, 'client/storybook-static', 'index.html')); 
  
 
}); 

const port = process.env.PORT || 8080; 

app.listen(port); 




•	We need to start the storybook build from client folder. This can be achieved by adding post install script in package.json like below. This will start the buildClient script.  



"postinstall": "cd client && npm run buildClient"  



•	The above buildClient will run the client_build.sh which contains below. It will start npm install, once this is done, we need to run storybook build 

•	rm -rf node_modules 

•	echo "Installing npm modules" 

•	npm install 



•	To start the storybook build, add  post Install build command. This will create a folder called storybook-static which will be passed to express.static. 

    •	"buildstorybook": "build-storybook -c .storybook -s assets", 
    
    •	"postinstall": "npm run buildstorybook", 
    

