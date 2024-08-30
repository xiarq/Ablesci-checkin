#!/usr/bin/env python
# coding=utf-8
'''
Author: JY
Date: 2023-12-27 18:30:32
LastEditTime: 2023-12-27 21:02:08
LastEditors: JY
Description: 
FilePath: /Ablesci-checkin/main.py
'''
#!/usr/bin/env python
# coding=utf-8
import requests
import os
import json

env = os.environ.get("CONFIG")


def ablesci(headers):
    url = "https://www.ablesci.com/user/sign"
    response = requests.get(url, headers=headers)
    if response.status_code == 200:
        msg = response.json()["msg"]
        return msg
    else:
        return None



if __name__ == "__main__":
    config_path = os.path.join(os.path.dirname(__file__), "config.json")
    if os.path.exists(config_path):
        with open(config_path, "r", encoding="utf-8") as f:
            config = json.loads(f.read())
    else:
        config = json.loads(env)

    _check_item = config.get("ablesci", [])[0]
    pushToken = config.get("PUSHTOKEN", [])

    Cookie = _check_item.get("cookie", [])
    headers = {
        "Accept": "application/json, text/javascript, */*; q=0.01",
        "Accept-Encoding": "gzip, deflate, br",
        "Accept-Language": "zh-CN,zh;q=0.9",
        "Cookie": f"{Cookie}",
        "DNT": "1",
        "Referer": "https://www.ablesci.com/",
        "Sec-Fetch-Dest": "empty",
        "Sec-Fetch-Mode": "cors",
        "Sec-Fetch-Site": "same-origin",
        "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/112.0.0.0 Safari/537.36",
        "X-Requested-With": "XMLHttpRequest"
    }

    response_data = ablesci(headers)
    if response_data is not None:
        content = response_data
        if pushToken is not None:
            requests.post('https://www.pushplus.plus/send', {'token': pushToken, 'title': '科研通签到', 'content': content})
    else:
        print("Unable to get response data from ablesci.")
