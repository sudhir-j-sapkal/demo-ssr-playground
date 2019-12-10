## Playground for SSR and Prerendering with Angular

### Installing and building

Install all dependencies as usual.
Just to make sure everything is fine, run the project locally:

```bash
npm install
ng serve
```

If you want, you can take a look at the HTML source code in the browser. It should show the typical `index.html` skeleton with an empty `<app-root></app-root>` element.

We then need separate builds for client and server.

```bash
# Client
ng build --prod

# Server
ng run ssr-playground:server:production --bundleDependencies all


# OR both together
npm run build:client-and-server-bundles
```

You should now find a `dist` folder with two sub-directories:

```
- dist
    - browser
    - server
```

We can take a look at the server now!

### Compiling the server for SSR

The server part is a TypeScript program for Node.js in the `server.ts` file.
In order to bring everything together, we need to bundle the server application using webpack.
Everything is already prepared as NPM run scripts:

```bash
npm run compile:server
```


### Running Server-side rendering

Run the Express server with live server-side rendering:

```bash
node dist/server/main
```

Open your browser at [http://localhost:4000](http://localhost:4000) to see it in action. When you show the source code in the browser you should see the server-side rendered HTML.


#### Pre-rendering


```bash
npm run prerender
```

You should now find some subfolders in the `dist/browser` directory, according to the routes of the application.
Run a local web server there, e.g. `http-server`:

```bash
cd dist/browser
npx http-server

# OR if you have http-server installed globally
http-server
```

Open your browser at [http://localhost:8080](http://localhost:8080).
This should be blazing fast because it just shows the prerendered pages without doing any rendering at runtime.
The Angular application bundles will kick in later and take over the static page.


