# The generated static site

## How it works?

THe SPA is configured using [this](https://github.com/rafgraph/spa-github-pages).

## Making an update and deploying

1) Make sure app.json has

    ```json
    "experiments": {
        "baseUrl": "/tribe-mate-web/"
    },
    ```

2) Make sure redirect URL in both GCP as well as the web app has redirect uri as `https://tribe-mate.github.io/tribe-mate-web/signup/`:

    ```tsx
    const [, response, promptAsync] = Google.useAuthRequest({
        iosClientId: CLIENT_IDS.ios,
        webClientId: CLIENT_IDS.web,
        androidClientId: CLIENT_IDS.android,
        redirectUri: Platform.select({
        web: "https://tribe-mate.github.io/tribe-mate-web/signup/",
        default: undefined, // Let Expo handle redirect URIs on native platforms
        }),
    });
    ```

3) Generate the static files using:

    ```bash
    npx expo export -p web
    ```

    this will generate a dist folder.

4) Copy the bundle js from this dist to expo/ dir here. Make sure to not change `expo` dir to `_expo`

5) Update the dist name in `index.html`
