## The common snippets of the javascript

* 动态加载javascript

```javascript
  function loadScript(url, callback){
    var script = document.createElement('script');
    script.type = 'text/javascript';

    if(script.readyState){ //IE
      script.onreadystatechange = function(){
        if(script.readyState === 'loaded' || script.readyState === 'complete'){
          script.onreadystatechange = null;
          callback()
        }
      }
    }else{ //Others
      script.onload = callback.call(this);
    }

    script.url = url;
    document.getElementsByTagName('head')[0].appendChild(script);
  }
```

> From:[The best way to load external JavaScript](https://www.nczonline.net/blog/2009/07/28/the-best-way-to-load-external-javascript/)
