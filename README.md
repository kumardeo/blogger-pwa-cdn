# Blogger PWA using CDN

Build a PWA application for your Blogger blog using CDN services like [JsDelivr](https://www.jsdelivr.com).

Works with `blogspot.com` subdomains.

## Getting Started

You can follow these few steps:

### 1. Fork Repository

Fork this repository with an appropriate name. You can name the repository same as the blog name.

> If you don't have a Github account yet, create one and fork this repository.

### 2. Upload Favicons

1. Prepare an icon for your blog in `.png` extension with a size of `512x512` (recommended file size: maximum `150KiB`).
   * Rename the file as `android-icon-512x512.png`

2. Go to [favicon-generator.org](https://www.favicon-generator.org/) and generate favicons by uploading the blog icon.

3. Download the generated favicon and extract the files.
   * Delete unnecessary files: `browserconfig.xml`, `manifest.json`

4. Upload these icons in `public/icons` directory in the main branch of forked repository.
   * Upload the original file as well, i.e. `android-icon-512x512.png`.
   * Total number of icons will be approximately `26`.

### 3. Upload Screenshots

1. Prepare `5` screenshots of your Webpages of size `540x720` in `.png` extension that will appear when it shows the install button (recommended file size: maximum `750KB each`).

2. Name the screenshots in series:
   * `screen-1.png`
   * `screen-2.png`
   * `screen-3.png`
   * `screen-4.png`
   * `screen-5.png`

3. Upload all these screenshots in `public/screenshots` directory in the main branch of forked repository.

### 4. Update manifest.json

1. Go to forked repository and open `public/manifest.json` file.

2. The file looks something like the following:
   https://github.com/armaan-kumar/blogger-pwa-cdn/blob/a4753c91d7eb9c552732f3ef744540bcbe159950/public/manifest.json#L1-L122

3. Replace the blog name, urls, etc. with your blog url.
   * You can also add your custom `screenshots`, `icons`, etc. Refer to [Mozilla Docs](https://developer.mozilla.org/en-US/docs/Web/Manifest).

### 5. Edit Template XML

1. Now go to Blogger Dashboard. Go to `Theme` section.

2. Click on `Edit HTML`.

3. Paste the following codes below `<head>`, if you didn't find it, it would have been probably parsed which is `&lt;head&gt;`.

   ```html
   <!--[ START: PWA Meta Tags]-->
   <link href="https://cdn.jsdelivr.net/gh/USERNAME/REPOSITORY/public/icons/apple-icon-57x57.png" rel="apple-touch-icon" sizes="57x57" />
   <link href="https://cdn.jsdelivr.net/gh/USERNAME/REPOSITORY/public/icons/apple-icon-60x60.png" rel="apple-touch-icon" sizes="60x60" />
   <link href="https://cdn.jsdelivr.net/gh/USERNAME/REPOSITORY/public/icons/apple-icon-72x72.png" rel="apple-touch-icon" sizes="72x72" />
   <link href="https://cdn.jsdelivr.net/gh/USERNAME/REPOSITORY/public/icons/apple-icon-76x76.png" rel="apple-touch-icon" sizes="76x76" />
   <link href="https://cdn.jsdelivr.net/gh/USERNAME/REPOSITORY/public/icons/apple-icon-114x114.png" rel="apple-touch-icon" sizes="114x114" />
   <link href="https://cdn.jsdelivr.net/gh/USERNAME/REPOSITORY/public/icons/apple-icon-120x120.png" rel="apple-touch-icon" sizes="120x120" />
   <link href="https://cdn.jsdelivr.net/gh/USERNAME/REPOSITORY/public/icons/apple-icon-144x144.png" rel="apple-touch-icon" sizes="144x144" />
   <link href="https://cdn.jsdelivr.net/gh/USERNAME/REPOSITORY/public/icons/apple-icon-152x152.png" rel="apple-touch-icon" sizes="152x152" />
   <link href="https://cdn.jsdelivr.net/gh/USERNAME/REPOSITORY/public/icons/apple-icon-180x180.png" rel="apple-touch-icon" sizes="180x180" />
   <link href="https://cdn.jsdelivr.net/gh/USERNAME/REPOSITORY/public/icons/favicon-16x16.png" rel="icon" type="image/png" sizes="16x16" />
   <link href="https://cdn.jsdelivr.net/gh/USERNAME/REPOSITORY/public/icons/favicon-32x32.png" rel="icon" type="image/png" sizes="32x32" />
   <link href="https://cdn.jsdelivr.net/gh/USERNAME/REPOSITORY/public/icons/favicon-96x96.png" rel="icon" type="image/png" sizes="96x96" />
   <link href="https://cdn.jsdelivr.net/gh/USERNAME/REPOSITORY/public/icons/android-icon-192x192.png" rel="icon" type="image/png" sizes="192x192" />
   <link href="https://cdn.jsdelivr.net/gh/USERNAME/REPOSITORY/public/manifest.json" rel="manifest" />
   <meta content="yes" name="mobile-web-app-capable" />
   <meta content="My Blog" name="application-name" />
   <meta content="#ffffff" name="theme-color" />
   <meta content="yes" name="apple-mobile-web-app-capable" />
   <meta content="My Blog" name="apple-mobile-web-app-title" />
   <meta content="black-translucent" name="apple-mobile-web-app-status-bar-style" />
   <!--[ END: PWA Meta Tags ]-->
   ```

   * Replace `My Blog` with your blog title, `USERNAME` with your GitHub username and `REPOSITORY` with the repository name.
   * Delete existing similar codes.

4. Save the changes.

### 6. Custom Install Button (Optional)

You may want to add a custom button on your site which shows the installation prompt on click. You can use the following css and javascript codes to create a beautiful install button.

> **Warning** You should not use it if you are using an AMP template.

1. Add the following css in Template XML just above to `</head>`:

   ```html
   <style>/*<![CDATA[*/
   /*! Custom PWA install button by Fineshop Design */
   .pwa-button{position:fixed;z-index:999;left:20px;bottom:75px;display:flex;align-items:center;justify-content:center;width:40px;height:40px;border:none;border-radius:50%;background:#1900ff;visibility:visible;opacity:1;transition:visibility .5s,opacity .5s}
   .pwa-button[hidden]{display:flex;visibility:hidden;opacity:0}
   .pwa-button:not([disabled])::before{content:'';position:absolute;z-index:-1;inset:0;background:inherit;border-radius:inherit;animation:1s cubic-bezier(0,0,.2,1) infinite pwa-button-ping}
   .pwa-button svg.flash{width:22px;height:22px;fill:none;stroke:#fff;stroke-linecap:round;stroke-linejoin:round;stroke-width:1.4}
   @keyframes pwa-button-ping{75%,to{transform:scale(1.6);opacity:0}}
   /*]]>*/</style>
   ```

2. Add the following javascript just above to `</body>`:

   ```html
   <script type='module'>/*<![CDATA[*/
   /*! Custom PWA install button by Fineshop Design */
   (({button:t,onInstall:n})=>{let i=null;var e=()=>{i&&(t.disabled=!0,i.prompt().then(e=>{"accepted"===e.outcome&&o()}).finally(()=>{t.disabled=!1}),i=null)},l=e=>{e.preventDefault(),i=e,t.hidden=!1};const o=()=>{t.hidden=!0,t.removeEventListener("click",e),window.removeEventListener("beforeinstallprompt",l)};t instanceof HTMLElement&&(t.hidden=!0,t.addEventListener("click",e),window.addEventListener("beforeinstallprompt",l));const d=e=>{t instanceof HTMLElement&&o(),"function"==typeof n&&n(e),window.removeEventListener("appinstalled",d)};window.addEventListener("appinstalled",d)})({
     button: document.getElementById("app_install_button")||Object.assign(document.body.appendChild(document.createElement("button")),{hidden:!0,type:"button",className:"pwa-button",innerHTML:"<svg class='flash' viewBox='0 0 24 24'><path d='M6.08998 13.28H9.17998V20.48C9.17998 22.16 10.09 22.5 11.2 21.24L18.77 12.64C19.7 11.59 19.31 10.72 17.9 10.72H14.81V3.52002C14.81 1.84002 13.9 1.50002 12.79 2.76002L5.21998 11.36C4.29998 12.42 4.68998 13.28 6.08998 13.28Z' stroke-miterlimit='10'></path></svg>"}),
     onInstall(){
       /**
        * Do something on app installed
        * i.e. Display a Thank You message in UI
        */
     }
   });
   /*]]>*/</script>
   ```

3. Save the changes, now an install button will appear on your site.

## Purging Cache

JsDelivr caches files on their server so if you update any file on GitHub, it will be updated on the server instantly.  

In that case you manually need to tell JsDelivr to purge cache. You can use this JsDelivr's [Purge Cache Tool](https://www.jsdelivr.com/tools/purge) to do so.

## Caveats

You can build a PWA app using it but you can't do the following since it requires resources from same origin:

1. **Offline Page**: The app will show default interface of the web view when user is not connected to internet.
   * It is because it needs Server Worker (which cannot be registered from different origin).

2. **Push Notification**: You cannot use third party Push Notification services (i.e. OneSignal) to send push notifications from same domain of the app.
   * Push notifications are possible with Service Worker.

## License

The project is licensed under MIT License.
