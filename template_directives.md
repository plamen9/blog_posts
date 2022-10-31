# Wider Support for Template Directives

> You can now use Template Directives in HTML Expressions of Classic and Interactive Report columns, enabling you to remove conditional output logic from your SQL queries. [Learn more about `Template Directives`](https://docs.oracle.com/en/database/oracle/apex/22.1/htmdb/using-template-directives.html)<br>
Also check [Jon Dixon](https://blog.cloudnueva.com/)'s blog post on [Template Directives](https://blog.cloudnueva.com/apex-template-directives).

One of my personal favourites. For a long time, the only options to format Report data with some custom HTML was to do it directly in the select statement or to create a custom Template in Shared Components.

Having the `Template Directives` tackled that and I am using it whenever possible. Here is an example:

![template_directives.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1667234672999/Z4emZeVnZ.jpg)

```html
{case SOURCE/}
{when strava/}
<img width="28px" alt="#SOURCE#" title="#SOURCE#" src="#APP_IMAGES#icons/strava_logo_64_64.png">
{when fitness_challenge_app/}
<img width="28px" alt="#SOURCE#" title="#SOURCE#" src="#APP_IMAGES#icons/app_icon_64_64.png">
{otherwise/}
<span>#SOURCE#</span>
{endcase/}
```

What this template does is check the value of my Report `SOURCE` column and applies different HTML based on the value. 

The benefit is that your Report `SQL` query still looks pretty, and at the same time you have the conditional output on your page.

Let's hope `Template Directives` continue to be supported in more and more APEX components! 
