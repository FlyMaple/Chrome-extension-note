# Chrome Extension

## Ref
[JavaScript API](https://crxdoc-zh.appspot.com/extensions/api_index)

## browserAction
``` JS
(function () {
    'use strict';

    function BrowserActionClick(tab) {
        chrome.tabs.executeScript({
            code: 'document.body.style.backgroundColor="red"'
        })
    }

    function getTitle(title) {
        console.log(title);
    }

    function getPopup(popup) {
        console.log(popup);
    }

    function getBadgeText(text) {
        console.log(text);
    }

    function getBadgeBgColor(color) {
        console.log(color);
    }

    chrome.browserAction.onClicked.addListener(BrowserActionClick);
    
    chrome.browserAction.setTitle({ title: 'setTtitle' });
    chrome.browserAction.getTitle({}, getTitle)
    chrome.browserAction.setPopup({ popup: 'popup.html' });
    chrome.browserAction.getPopup({}, getPopup);
    chrome.browserAction.setBadgeText({ text: 'ABC' });
    chrome.browserAction.getBadgeText({}, getBadgeText);
    chrome.browserAction.setBadgeBackgroundColor({ color: '#903aaa' })
    chrome.browserAction.getBadgeBackgroundColor({}, getBadgeBgColor);

    chrome.browerAction.disable(3595);
    chrome.browerAction.enable(3595);
})();
```

## pageAction
``` JS
(function () {
    'use strict';

    chrome.pageAction.show(tabId);
    chrome.pageAction.hide(tabId);
    chrome.pageAction.onClicked.addListener(xxx);
})();
```

``` JSON
"page_action": {
    "default_icon": "images/icon.png",
    "default_title": "There's a <video> in this page!"
}
```

## Notifications
``` JS
(function () {
    'use strict';

    function BrowserActionClick() {
        if (window.Notification) {
            var instacne = new Notification('Title', {
                icon: 'images/icon.png',
                body: 'This is Body.'
            });
        }
    }

    chrome.browserAction.setPopup({ 'popup': '' });

    chrome.browserAction.onClicked.addListener(BrowserActionClick);
})();
```

``` JSON
"permissions": [
    "notifications"
],
"web_accessible_resources": [ 
    "images/icon.png"
]
```

## Omnibox
``` JS
(function () {
    'use strict';
    
    function OmniboxStarted() {
        console.log('start');
    }

    function OmniboxEnterd(input) {
        console.log(input);
    }

    function OmniboxCanceled() {
        console.log('cancel');
    }

    function OmniboxChanged(input, suggest) {
        console.log('input: ' + input);
        suggest([
            { content: "open new tab", description: "This is First Command." },
            { content: "close out system", description: "This is Second Command." }
        ]);
    }

    chrome.omnibox.onInputStarted.addListener(OmniboxStarted);
    chrome.omnibox.onInputEntered.addListener(OmniboxEnterd);
    chrome.omnibox.onInputCancelled.addListener(OmniboxCanceled);
    chrome.omnibox.onInputChanged.addListener(OmniboxChanged);
})();
```

``` JSON
"omnibox": { "keyword": "aaron" }
```

## theme
``` JSON
"theme": {
    "images" : {
        "theme_frame" : "images/theme_frame_camo.png",
        "theme_frame_overlay" : "images/theme_frame_stripe.png",
        "theme_toolbar" : "images/theme_toolbar_camo.png",
        "theme_ntp_background" : "images/theme_ntp_background_norepeat.png",
        "theme_ntp_attribution" : "images/attribution.png"
    },
    "colors" : {
        "frame" : [71, 105, 91],
        "toolbar" : [207, 221, 192],
        "ntp_text" : [20, 40, 0],
        "ntp_link" : [36, 70, 0],
        "ntp_section" : [207, 221, 192],
        "button_background" : [255, 255, 255]
    },
    "tints" : {
        "buttons" : [0.33, 0.5, 0.47]
    },
    "properties" : {
        "ntp_background_alignment" : "bottom"
    }
}
```

## Cookies
``` JS
(function () {
    'use strict';
    
    var url = 'https://cmsdev02.aegislab.com/netgear_portal/index.html';
    var name = 'cExt';

    function getCookie(cookies) {
        console.log(cookies);
    }

    function getAllCookie(list) {
        console.log(list);
    }

    function getAllCookieStores(list) {
        console.log(list);
    }

    function CookieChanged(changeInfo) {
        console.log(changeInfo);
    }


    chrome.cookies.get({ url: url, name: name }, getCookie);
    chrome.cookies.getAll({ url: url }, getAllCookie);
    chrome.cookies.set({ url: url, name: name, value: 'xXx' });
    chrome.cookies.remove({ url: url, name: name });
    chrome.cookies.getAllCookieStores(getAllCookieStores);
    chrome.cookies.onChanged.addListener(CookieChanged);
})();
```

``` JSON
"cookies",
"http://*/*",
"https://*/*",
```

## tabs

## windows

## Other
``` JS
var link = jQuery('<link>');
link.attr('rel', 'stylesheet');
link.attr('type', 'text/css');
link.attr('href', 'chrome-extension://' + extId + '/css/general.css');
document.head.appendChild(link[0]);

var script = document.createElement('script');
script.setAttribute('src', 'chrome-extension://' + extId + '/js/TRA_contentScript.js');
document.head.appendChild(script);
```
