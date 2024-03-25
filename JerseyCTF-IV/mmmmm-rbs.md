---
ctf: Jersey CTF
ctf-website: https://ctf.jerseyctf.com/
challenge: mmmmm-rbs
category: web
author: ott
---
# mmmmm-rbs

>Dr. Tom Lei is up to something again and it's not sounding good. We heard he was messing around over at [https://drtomlei.xyz](https://drtomlei.xyz/). Maybe we should look into this.
>
>Developed by: [Cyb0rgSw0rd](https://github.com/AlfredSimpson)

# Solution

Initially going to the website, we see some sort of blog home page.

![home page](./mmmmm-rbs-home.png)

Navigating to the `/about` page, it gives us an unauthorized error.

![about page](./mmmmm-rbs-about.png)

Viewing the source reveals the `/img/` directory, but that's a 404 as well.

<view-source:https://drtomlei.xyz/>
<view-source:https://drtomlei.xyz/about>

Looking into the network tab on the initial request we see a cookie 

```
yummyflag=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmbGFnIjoiamN0ZntnMXYzX20zX3RoM19iMzNmX25fY2gzZGRAcl9wbHp9IiwiaWF0IjoxNzExMzA2NDkxfQ.Bk8gATf5teDucZFrlMh-eAd9HIODeAfChjt0pKAR9Xk; Path=/; HttpOnly; SameSite=Strict
```

![network tab](./mmmmm-rbs-network-tab.png)

The cookie value `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmbGFnIjoiamN0ZntnMXYzX20zX3RoM19iMzNmX25fY2gzZGRAcl9wbHp9IiwiaWF0IjoxNzExMzA2NDkxfQ.Bk8gATf5teDucZFrlMh-eAd9HIODeAfChjt0pKAR9Xk` looks like a [JWT](https://jwt.io) because its a long-ish base64 encoded string with 3 sections separated by `.`s.

Checking the [JWT Debugger](https://jwt.io) we see the JWT has the key `flag`.

```
{
  "flag": "jctf{g1v3_m3_th3_b33f_n_ch3dd@r_plz}",
  "iat": 1711306491
}
```

![jwt debugger](./mmmmm-rbs-jwt-debugger.png)
