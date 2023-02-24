# Development design implementation

### App
- 404
- at least global `meta title` and `meta description`
- there is global error handler if necessary
- check with real android & iOS devices
- check asset directory if some are unreasonably big
- check if it needs to have analytics
- has favicon.ico

### Pages
- make optimal choice between api calls that are server or client rendered
- section spacings are consistent
- check all responsive versions
- if page has some kind of `id` param make sure it returns 404 on not found
- check page bundle size when building on CI/CD
- check if pages are static that need to be static on CI/CD
- run lighthouse and check `SEO` and best `practices` and fix accordingly
- check if every page has one `<h1>` tag
- inputs have validation errors
- modals have body scroll lock `https://www.npmjs.com/package/body-scroll-lock`
- important modals that have to be crawled have deep link

### CI/CD
- define if it has staging server
- define if it has tests
