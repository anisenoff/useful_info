This is info from Arjun abt how to enable the experimental flags for Chrome

````python
options = webdriver.ChromeOptions()

local_state = {
    "browser": {
        "enabled_labs_experiments": [
            "enable-fenced-frames-developer-mode@1",
            "enable-fenced-frames@1",
            "privacy-sandbox-ads-apis",
            "privacy-sandbox-enrollment-overrides"
        ],
        "enabled_labs_experiments_origin_lists": {
            "privacy-sandbox-enrollment-overrides": "https://cups.cs.cmu.edu,https://www.andrew.cmu.edu,https://anisenoff.github.io"
        },
    },
}

options.add_experimental_option("localState", local_state)
driver = webdriver.Chrome(options=options)
driver.get("chrome://flags")

````

also, if you want to make changes to the dict, the easiest way is to enable the flags on chrome, and then run this command to get the updated local state
```cat $HOME/Library/Application\ Support/Google/Chrome/Local\ State | jq .browser```
