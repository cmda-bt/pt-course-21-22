# Heroku troubleshooting

This file contains a list of common errors or crashes when uploading your website to Heroku. You should consult this file every time your logs on Heroku display some form of `changed status from started to crashed` or similar.
Please do note, it is still your task to troubleshoot and solve your error. If the error you've encountered is not included in the list, please let us know in the Teams channel so we can add it. Do not forget to take a screenshot beforehand.

<hr>

## Missing .env or "config vars" (_cannot read property x of y_)

![Common error message when handling config vars](assets/errors/config-vars.png)

This error usually states something like _undefined_ or _invalid key_ or _unable to connect to Heroku_. This happens because Heroku has their own way of entering the environment variables. In Heroku, go to settings and scroll down until you see the button "Reveal Config Vars". This button enables you to enter your own .env content into Heroku.

The specific error your see here is due to a missing API key for an exteral API, because the error isn't correctly captured, and the response isn't valid JSON, the application will crash and display an application error when revisited. This could also happen when your connection to MongoDB or similar instances is not working.

<hr>

## Crashed on starting due to nodemon not found

![Common error message when using nodemon](assets/errors/config-vars.png)

Nodemon is a devDependency tool that allows us to restart the server when changes to the files have been made. It is a great development tool to speed up debugging and testing. However, it is not applicable when the server is already live, say on Heroku. Heroku has their own methods in place to ensure the server always stays up, even after accidentally crashing. In order to fix this error, you should change the content of your `package.json` starting script from `nodemon <index> / <server> / <app>.js` to node `node <index> / <server> / <app>.js`. If you still wish to continue using nodemon in your development environment, you should add another script, something like `dev` that uses `nodemon <index> / <server> / <app>.js`.
