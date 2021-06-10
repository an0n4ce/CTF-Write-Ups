# Fun with Tokens

![](img/chal.png)

Challenge [Link](http://3.142.122.1:9334/)

![](img/1.png)

The challenge is about JWT Token. Let's check the source code.

![](img/2.png)

Going through that source code we know there is a `/login` , `/adminNames` , `/admin` directories. from `/adminNames` we get file to download.

![](img/3.png)

It's look like some credentials to login.

![](img/4.png)

Let's check on `/login` page. login with given creds that is `username=din_djarin11` and `password=0xd4127c3c`. From the headers there is something interesting. There we see a header named `token`
```
token: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InF2YV9xd25ldmExMSIsInBhc3N3b3JkIjoiMGtxNDEyN3AzcCIsImFkbWluIjoic255ZnIiLCJpYXQiOjE2MjMzMjkwMDh9.T00vse0IDBF5_JFxj7jr7XTIegQdW3MtFN33fXpNW8U
```

![](img/6.png)

It's JWT Token. Here i used [jwt.io](https://jwt.io/) to decode that token.

![](img/7.png)

We can see here username and password is encoded to `ROT13` cipher. Now we need `SIGNATURE` key to verify. When we get file named `admins` there is `file=` parameter to get file. that is `/getFile?file=admins`. maybe there is chance for `LFI` vulnerability. Let's look that to get something interesting file.

![](img/10.png)

I looked for `index.js` file it shows `file name is too big`. also we can know it's a `Express.js` application so maybe a chance to get `.env` file.
After some failed attempts i get `.env` file from `file=../.env`.

![](img/11.png)

This will be the SIGNATURE key `G00D_s0ld13rs_k33p_s3cret5`.

Let's Look on `/admin`

![](img/8.png)

That message saying somthing interesting about headers. Before that we need to do somthing on our token, We need add SIGNATURE key. And the payload `admin` value is `false`, change that into `true` with `rot13` encoded string `gehr`. let's create the token.

![](img/12.png)

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InF2YV9xd25ldmExMSIsInBhc3N3b3JkIjoiMGtxNDEyN3AzcCIsImFkbWluIjoiZ2VociIsImlhdCI6MTYyMzMyNjkxM30.G9YsYruNHT6pJ464dggn0SmA0xiPs_OGlalAgcK1Zbo
```
On `/admin` we need to edit and add header called `Authorization: ` add token there. and resend the request with browser `Network Monitor`.

![](img/13.png)

From the responce tab we get `rot13` encoded flag.

![](img/14.png)

Decode to get our flag.

![](img/flag.png)

```SHELL{T0k3ns_d0_m4tt3r_4e91af4506f384d460f0f0c6e9e5fe4a}```
