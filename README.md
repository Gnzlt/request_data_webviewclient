Request Data - WebViewClient
====================
Android WebViewClient with a custom WebResourceRequest that contains the POST/PUT/... payload of XMLHttpRequest requests

This project is inspired by https://github.com/KeejOow/android-post-webview and draws some code from there.


When you need to display a webview to the user on which you need to intercept the HTTP calls and perform them yourself (for example to add additional security), you can do so on Android by registering a `WebViewClient` and implementing 

```
android.webkit.WebViewClient#shouldInterceptRequest(android.webkit.WebView webview, WebResourceRequest request)
```

Unfortunately, the `request object passed to this method` does not contain any POST data, wich is needed when proxying the request.

This project provides a hack around this limitation by injecting into the HTML that intercepts AJAX calls.

It provides the `WriteHandlingWebViewClient` class that extends `WebViewClient` and provides the 
```
public WebResourceResponse shouldInterceptRequest(final WebView view, WriteHandlingWebResourceRequest request)
```
method to override.

`WriteHandlingWebResourceRequest` extends `WebResourceRequest`, but provides the crucial method
```
public String getAjaxData()
```
which returns the data in the request body of the AJAX request.


# Installation

 * Add the `writeinterceptingwebview` folder as a libarary module to your android project. 
 * (jCenter/Maven package is in the works)
 