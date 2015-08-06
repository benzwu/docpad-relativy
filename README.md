# docpad-relativy

## problem

To create a browsable local copy of docpad output, url link must be converted to path relative link.

    current folder (Relative to the root)
    /blog/super/post1.html

    refer to: /css/all.min.css

    must be converted to
    ../../css/all.min.css

## code

put this code in your docpad.coffee under templateData

```
    templateData:
    
        relativy: (x) ->
             if @document.url is x
                 return "#top"
             doca=@document.url.split "/"
             lnka=x.split "/"
             c=-1
             c++ while (doca[c] is lnka[c]) and (c<55)
             if c>50
                 console.log("warning", "relativy endless loop")
                 return "ERROR"
             u=""
             if c <= doca.length-2
                 for i in [c..(doca.length-2)]
                     u+="../"
             if c <= (lnka.length-2)
                 for i in [c..lnka.length-2]
                     u+=lnka[i]+"/"
             u+=lnka[lnka.length-1]
             u
```

## implementation

Pass all your url to the function

example:

````
<%=@relativy("/icon/dcbanner.gif")%>
````

result will be depend on document url


