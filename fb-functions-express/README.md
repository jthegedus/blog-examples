# Express Server on Cloud Functions for Firebase

Host an Express Server in Cloud Functions for Firebase.

Here is the accompanying [Medium Post](https://medium.com/@jthegedus/express-js-on-cloud-functions-for-firebase-86ed26f9144c).

## TLDR;

Host your Express Server on Cloud Functions enabling a low-cost, auto-scaling web server leveraging Firebase's sweet developer experience.

Cloud Functions uses [Express request and response objects](https://firebase.google.com/docs/functions/http-events#trigger_a_function_with_an_http_request) allowing us to pass an Express app [directly into the function](https://github.com/jthegedus/firebase-functions-express-example/blob/master/firebase-functions-express/src/functions/index.js#L11).

## Download & Install

```shell
curl https://codeload.github.com/jthegedus/blog-code/tar.gz/master | tar -xz --strip=1 firebase-gcp-examples-master/fb-functions-express
cd firebase-functions-express
# Install
yarn
```

## Login to the Firebase CLI

If you're using `firebase-tools` globally, then skip to the [_Deploy to Firebase_](#deploy-to-firebase) step.

```shell
yarn fblogin
```

## Local Testing

`yarn funcs:serve` requires that the functions have been deployed:

```shell
yarn funcs:serve
```

Try the new experimental Firebase Shell for truly local testing:

```shell
yarn funcs:shell
```

## Deploy to Firebase

Update `.firebaserc` to use your Firebase project id.

```
yarn funcs:deploy
```

This will run the `prefuncs:deploy` script found in `firebase.json` which in turn executes some npm scripts from `package.json`. These scripts simply clean the `dist` folder, and then copy the `package.json` and `yarn.lock` to the folder where the functions will be so it has it's dependencies packaged with it. Eg:

```shell
./dist/
  | functions/
    | index.js
    | package.json
    | yarn.lock

# these files are copied to the dist/ folder
./package.json
./src/
  | functions/
    | index.js
./yarn.lock
```
