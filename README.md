# Uniform starter kit for Sitecore MVC and Next.js

This repo contains both the starter kit with content items and required configuration files.

This kit can be used to complete the official tutorial and to kick off a new project. There are minimal dependencies in this kit, and not functional components.

## Docs

1. [Tutorial for this starter kit](https://docs.uniform.dev/sitecore/deploy/getting-started/sitecore-mvc-tutorial)

1. [Uniform for Sitecore docs](https://docs.uniform.dev/sitecore/deploy/introduction/)

## Pre-requisites
1. Sitecore 9.3 - 10.x instance.
1. "Uniform for Sitecore" installed and configured on your Sitecore instance. Check out the docs.
1. Install the Sitecore package with items from `/sitecore/App_Data/packages` folder.
1. (optional) To enable Optimize, 
   * modify the Views/MvcSite/Layout.cshtml according to [actual Optimize documentation](https://docs.uniform.dev/sitecore/../#add-tracker-to-layout-view)
   * enable `uniform-mvc-kit.Uniform.Deployment.Media.Uniform.OptimizeIntegration.config.disabled` config in `sitecore/App_Config/Include/zzz_uniform-mvc-kit` folder
   * enable and fill in `uniform-mvc-kit.Uniform.Deployment.Media.Uniform.PurgeCache.Akamai.config.disabled` config in `sitecore/App_Config/Include/zzz_uniform-mvc-kit` folder
   * download and place `uniform.optimize.min.js` file in `public/scripts` folder (important! not `scripts` but `public/scripts`)
1. Deploy the configs from `/sitecore/App_Config` folder to your Sitecore instance's `App_Config` folder (the subfolder structure should match).

## Getting started with the app

> Check out official docs for more scenarios and [tutorial](https://docs.uniform.dev/sitecore/deploy/getting-started/sitecore-mvc-tutorial).

### TL;DR version

1. Configure `.env` file according to your environment specifics (see `.env-example` file).
1. `npm install`
1. Add `NPM_TOKEN` environment variable with the value we provided you with.
1. `npm run start` to start the SSR server.
2. `npm run export` to run static export if used only with the Uniform Deploy-only capability.
3. `npm run export:esi` to run static export if used with the Uniform Optimize capability.

## Cloudflare worker setup
1. Install `@cloudflare/wrangler` npm package \
    `npm i @cloudflare/wrangler@1.19.2 -g` 
1. Create a Cloudflare account: https://dash.cloudflare.com/login 
1. Create a Cloudflare API token:
    * Follow the link: https://dash.cloudflare.com/profile/api-tokens
    * Select "Create Token" button
    * Select "Edit Cloudflare Workers" among API token templates
    * In a new "Create Token" window don't change any Permissions (they are predefined correctly); indicate "All Accounts" in Account Resources section and "All Zones" in Zone Resources section. Client IP Address Filtering section can be skipped.
    * Press "Continue To Summary" and then "Create Token" buttons.
    * **IMPORTANT!** Copy and save your API Token somewhere. It only shown once after the initial setup. 
    * Finalize the worker setup: navigate to the Workers page (Click Workers link on the right pane on the Cloudflare main page) and click the Setup button next to your worker name; Choose to proceed with free account on the next page

1. Enable config: `uniform-mvc-kit.Uniform.Deployment.Hosted.z.Cloudflare.config.disabled` and specify required variables:
    * update `CF_ACCOUNT_ID` with your Cloudflare account ID
    * update `CF_API_TOKEN` with created Cloudflare API token
    * update `CF_WORKER_NAME` with preferable worker name

1. If incremental deploy configured: enable config: `uniform-mvc-kit.Uniform.Deployment.Incremental.z.Cloudflare.config.disabled` and specify required variables:
    * update `PublicUrl` with your Cloudflare public url

1. Default Cloudflare worker domain: `https://<WORKER-NAME>.<CLOUDFLARE-ACCOUNT-NAME>.workers.dev`


