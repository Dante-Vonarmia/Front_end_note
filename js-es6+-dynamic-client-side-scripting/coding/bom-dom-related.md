# BOM / DOM related

## Browser

### is WeChat Browser

```javascript
export const isWeiXin = () => {
  return navigator.userAgent.toLowerCase().match(/microMessenger/i) == 'micromessenger'
}
```

### is Device Mobile

```javascript
export const isDeviceMobile = () => {
  return /android|webos|iphone|ipod|balckberry/i.test(navigator.userAgent.toLowerCase());
}
```

### is Data Scraping

```javascript
export const isSpider = () => {
  return /adsbot|googlebot|bingbot|msnbot|yandexbot|baidubot|robot|careerbot|seznambot|bot|baiduspider|jikespider|symantecspider|scannerlwebcrawler|crawler|360spider|sosospider|sogou web sprider|sogou orion spider/.test(navigator.userAgent.toLowerCase());
}
```

### is iOS

```javascript
export const isIos = () => {
  var uA = navigator.userAgent;
  if (uA.indexOf('Android') > -1 || uA.indexOf('Linux') > -1) {
    return false
  } else if (uA.indexOf('iPhone') > -1) {
    return true
  } else if (uA.indexOf('iPad') > -1) {
    return false
  } else if (uA.indexOf('Windows Phone') > -1) {
    return false
  } else {
    return false
  }
}
```

### is PC end

```javascript
export const isPC = () => {
  var userAgentInfo = navigator.userAgent;
  var Agents = ["Android", "iPhone", "SymbianOS", "Windows Phone", "iPad", "iPod"];
  var flag = true;
  for (var v = 0; v < Agents.length; v++) {
    if (userAgentInfo.indexOf(Agents[v]) > 0) {
      flag = false;
      break;
    }
  }
  return flag;
}
```

## DOM APIs

### Remove DOM tags part

```javascript
export const removeHtmltag = (str) => {
    return str.replace(/<[^>]+>/g, '')
}
```

### get url arguments

```javascript
export const getQueryString = (name) => {
    const reg = new RegExp('(^|&)' + name + '=([^&]*)(&|$)', 'i');
    const search = window.location.search.split('?')[1] || '';
    const r = search.match(reg) || [];
    return r[2];
}
```

### Is "class" inside of the "element"

```javascript
export const hasClass = (el, className) => {
    let reg = new RegExp('(^|\\s)' + className + '(\\s|$)')
    return reg.test(el.className)
}
```

### Add a "class" to the "element"

```javascript
export const addClass = (el, className) => {
    if (hasClass(el, className)) {
        return
    }
    let newClass = el.className.split(' ')
    newClass.push(className)
    el.className = newClass.join(' ')
}
```

### Remove a "class" to the "element"

```javascript
export const removeClass = (el, className) => {
    if (!hasClass(el, className)) {
        return
    }
    let reg = new RegExp('(^|\\s)' + className + '(\\s|$)', 'g')
    el.className = el.className.replace(reg, ' ')
}
```

### Get scroll coordinates

```javascript
export const getScrollPosition = (el = window) => ({
    x: el.pageXOffset !== undefined ? el.pageXOffset : el.scrollLeft,
    y: el.pageYOffset !== undefined ? el.pageYOffset : el.scrollTop
});
```

### Whether "el" is within the viewport

```javascript
export const elementIsVisibleInViewport = (el, partiallyVisible = false) => {
    const { top, left, bottom, right } = el.getBoundingClientRect();
    const { innerHeight, innerWidth } = window;
    return partiallyVisible
        ? ((top > 0 && top < innerHeight) || (bottom > 0 && bottom < innerHeight)) &&
        ((left > 0 && left < innerWidth) || (right > 0 && right < innerWidth))
        : top >= 0 && left >= 0 && bottom <= innerHeight && right <= innerWidth;
}
```

## URL Query

{% embed url="https://code-boxx.com/build-query-string-javascript/" %}
