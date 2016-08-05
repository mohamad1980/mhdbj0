# mhdbj0
Meteor-up

Production Quality Meteor Deployments 

Meteor Up (mup for short) is a command line tool that allows you to deploy any Meteor app to your own server. It supports only Debian/Ubuntu flavours and Open Solaris at the moments. (PRs are welcome)

#  Installation
    npm install -g mup
     
#  Creating a Meteor Up Project
    mkdir ~/my-meteor-deployment
    cd ~/my-meteor-deployment
    mup init
    
This will create two files in your Meteor Up project directory:


    mup.json - Meteor Up configuration file
    settings.json - Settings for Meteor's settings API

mup.json is commented and easy to follow (it supports JavaScript comments).
# Example File
    {
  // Server authentication info
  "servers": [
    {
      "host": "hostname",
      "username": "root",
      "password": "password",
      // or pem file (ssh based authentication)
      //"pem": "~/.ssh/id_rsa",
      // Also, for non-standard ssh port use this
      //"sshOptions": { "port" : 49154 },
      // server specific environment variables
      "env": {}
    }
  ],

  // Install MongoDB on the server. Does not destroy the local MongoDB on future setups
  "setupMongo": true,

  // WARNING: Node.js is required! Only skip if you already have Node.js installed on server.
  "setupNode": true,

  // WARNING: nodeVersion defaults to 0.10.43 if omitted. Do not use v, just the version number.
  "nodeVersion": "0.10.43",

  // Install PhantomJS on the server
  "setupPhantom": true,

  // Show a progress bar during the upload of the bundle to the server.
  // Might cause an error in some rare cases if set to true, for instance in Shippable CI
  "enableUploadProgressBar": true,

  // Application name (no spaces).
  "appName": "meteor",

  // Location of app (local directory). This can reference '~' as the users home directory.
  // i.e., "app": "~/Meteor/my-app",
  // This is the same as the line below.
  "app": "/Users/arunoda/Meteor/my-app",

  // Configure environment
  // ROOT_URL must be set to https://YOURDOMAIN.com when using the spiderable package & force SSL
  // your NGINX proxy or Cloudflare. When using just Meteor on SSL without spiderable this is not necessary
  "env": {
    "PORT": 80,
    "ROOT_URL": "http://myapp.com",
    "MONGO_URL": "mongodb://arunoda:fd8dsjsfh7@hanso.mongohq.com:10023/MyApp",
    "MAIL_URL": "smtp://postmaster%40myapp.mailgun.org:adj87sjhd7s@smtp.mailgun.org:587/"
  },

  // Meteor Up checks if the app comes online just after the deployment.
  // Before mup checks that, it will wait for the number of seconds configured below.
  "deployCheckWaitTime": 15
}
