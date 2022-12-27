# Medusa Q and A

The answers were picked from the Discord discussions we have in the community

The guide I am writing is [here](https://docs.google.com/document/d/1uPSHBadrBKatcycZrNLtVysF9zbSAE0F85ggS2uCU-8/edit?usp=sharing)

## I want to have multiple stores and one admin, how ?

Try sales channel

## I want to deploy medusa on Netlify, how ?

Use the same domain for the three instances

If you want to sell soemthing, you probably own a domain. So you should point that domain to your deployments. yourdomain.com to storefront. admin.yourdomain.com to admin. api.yourdomain.com to your backend deployment. 

Still storefront and admin can be on Vercel or Netlify

Be aware that Vercel doesn't allow commercial use for free. Netlify does

## How to run Medusa with PM2

`pm2 start npm --name "medusa-server" -- run start`

app_name: medusa-server

script_name: start (from package.json)

other way

`pm2 start "NODE_ENV=production npm run start"`

in our case 

```
cd my-medusa-store
pm2 start npm --name "medusa-server" -- run start
```

```
cd my-medusa-storefront
pm2 start npm --name "medusa-storefront" -- run dev
```

```
cd medusa-admin
pm2 start npm --name "medusa-admin" -- run dev
```

## What mean headless solution

A headless solution is decoupled from your frontend so that you can leverage whichever framework you're using.
Medusa gives you the engine plus some js tools to interact with it. What you'll do with is up to you.
You most likely don't want to use full url linking. In such cases you're losing the benefit of client side routing. 
Full url linking means a full website refresh.

I don't know what kind of framework you are using but you most likely will use something like Next.js, Remix, Astro or whatever
Then you can and should leverage its router and tools. 
You might use Remix nested routes: https://remix.run/docs/en/v1/guides/routing
Maybe Next.js static generation with client side routing. Or the new nested layouts routing.
In all those cases you want to use the handle property of the product object and use it for your routing.
You can check out nextjs medusa starter for inspiration.

## Gatsby or Next for the frontend

The nextjs is more up to date now. And AFAIK only this one will get future updates. For me next.js is far more superior then Gatsby. 

## Should I use vercel or netlify public domains

I would advise to not use vercel.app ,netlify.app domains

They are on the public suffix list, and because of that the server can't set the cookies needed for authentication, if the user accessing the site from most modern browsers such as Chrome, Firefox, etc. 

Public suffix list: https://publicsuffix.org/list/public_suffix_list.dat 

## How to troobleshoot Admin creds connection

- Install Medusa and seed the database with `--seed`
- Install Admin
- CORS
- Check that you are using the right url
  - If it's localhost use the right PORT 
  - If you are using a domain name use the subdomains
- Check that you are using https
- Cookies are set by the Admin and you can inspect that in the Dev Tools

## Hosting Medusa Solution

- First solution

I deploy on AWS and Azure but find it would be easier in Digital Ocean for beginners to deploy
[00:48]
My simplest environment is:

Medusajs server: Redis + EC2 (server hosting) + Postgres DB

Frontend: Nextjs : deployed on Vercel
Admin: Vite + React : deployed on Netlify or Vercel

- Second solution

1vcpu, 2GB RAM server with a swap file should handle medusa stack with no problem. Though I still would recommend at least 2 cores and 4GB RAM. Then scale up if needed.

Using Digital Ocean Spaces for hosting images but again you could spin up a MInio app in Dokku or Coolify in few minutes.

Using Dokku but Coolify works fine too

There's a opinion that databases, storage should be hosted elsewhere on managed instances (Managed Postgres, Redis, S3, Spaces).
But many companies are actually hosting all of those by themselves. It is actually very common to host everything on premise.
One thing I do is offsite database backups which I sync either to Digital Ocean Spaces or AWS S3.

- More tips

If you want to deploy Nextjs on your own VPS, here's your guide: https://github.com/serverless-stack/open-next/blob/main/README.md
