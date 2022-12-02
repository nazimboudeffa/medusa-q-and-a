# Medusa Q and A

Picked from the Discord

## I want to have multiple stores and one admin, how ?
Try sales channel

## I want to deploy medusa on Netlify, how ?
Use the same domain for the three instances

If you want to sell soemthing, you probably own a domain. So you should point that domain to your deployments. yourdomain.com to storefront. admin.yourdomain.com to admin. api.yourdomain.com to your backend deployment. 

Still storefront and admin can be on Vercel or Netlify

Be aware that Vercel doesn't allow commercial use for free. Netlify does
