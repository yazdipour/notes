- https://www.youtube.com/watch?v=BZeQETah684&index=2&list=PLCA101D6A85FE9D4B
- https://developer.chrome.com/extensions/getstarted
- https://developer.microsoft.com/en-us/microsoft-edge/platform/documentation/extensions/extension-api-roadmap/
- http://crxextractor.com/

* Isolated: Known as background Access all APIs  but no access to page or popup
    ```js
    "background": {"scripts": ["background.js"]},
    ```
* Extension: Script in popup
* User Page: Runs on user page
    ```js
    "content_scripts": [
                    {
                            "matches": ["http://www.instagram.com/*","https://www.instagram.com/*"],
                            "css": ["mystyles.css"],
                            "js": ["jquery.js", "myscript.js"]
                    }
            ]
    ```