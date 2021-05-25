# Choco Cookies

![](image/chall.png)

From the challenge name we know that it is something about `Cookie:` header.

![](image/webb.png)

From the webpage there is base64 encoded cookie value is storing flavour as name.

![](image/web.png)

Once we decode it we get `peanut`. 

![](image/web1.png)

From the Main webpage there is a hint `JK is only willing to eat a chocolate cookie` So let's encode `chocolate` to base64.

![](image/web3.png)

Then let's edit the Cookie value to base64 encoded string of chocolate.
`Cookie: flavour=Y2hvY29sYXRl` and resend the request.

![](image/web4.png)

After this we can get the flag in the `Responce Tab` of Browser's `Network Monitor`.

![](image/flag.png)

```flag = TamilCTF{cOoki3s_aRe_Fak3}```
