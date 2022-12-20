# Medusa Q and A

Picked from the Discord

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
pm2 start npm --name "medusa-admin" -- run start
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
