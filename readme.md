# appointment

This is a test project to get in touch with `vue` and the `google api`.
It will display the ten most recent appointments of a `google calendar`.

## requirements

latest version of [vue-cli][vue-cli].

    $ npm install -g @vue/cli

## first time preparations

For the first time run you must create an `oauth2 client id` in the [google api console][googleapiconsole].
You have to add your application url to the `authorized javascript sources` (e.g. http://localhost:8080) so that the authentication will work properly.

Like explained in the [vue-cli documentation][vueclidocenv], you must place a `.env.local` file in the projects root folder with

    VUE_APP_CLIENT_ID=<google_api_oauth2_client_id>

After everything is in place, you must install all dependencies.

    $ npm install

## build 

    $ npm run dev-build

builds a uncompressed version of `appointment`

    $ npm run build

will build a production version of `appointment`

## run

    $ npm run serve

will start `appointment` on `https://localhost:8080`.

## root uri

If you want to run this application with an other root uri, you can add/extend your `vue.config.js` with

    module.exports = {
        baseUrl: '/your/root/' 
    }

## Contact

Jan Frederik Hake, <jan_hake@gmx.de>. [@enter_haken](https://twitter.com/enter_haken) on Twitter.

[googleapiconsole]: https://console.developers.google.com
[vueclidocenv]: https://github.com/vuejs/vue-cli/blob/dev/docs/env.md
[vuecli]: https://github.com/vuejs/vue-cli
