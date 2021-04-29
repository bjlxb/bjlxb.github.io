---
layout: photo
title: Tornado框架Session封装
tags:
  - Django
date: 2021-04-28 11:49:18
categories: Django
photos:
---
Tornado框架官方没有提供Session相关方案，看到一个简单的封装，记录一下！
<!--more-->

```python

class Session(object):
    #request_handler_obj为当前RequestHandler对象的self参数#
    def __init__(self, request_handler_obj):

        # 先判断用户的session_id是否存在
        self._request_handler = request_handler_obj
        self.session_id = request_handler_obj.get_secure_cookie("session_id")

        # 如果不存在session_id,生成session_id
        if not self.session_id:
            self.session_id = uuid.uuid4().hex
            self.data = {}
            request_handler_obj.set_secure_cookie("session_id", self.session_id)

        # 如果存在session_id, 去redis中取出data
        else:
            try:
                json_data = request_handler_obj.redis.get("sess_%s" % self.session_id)
            except Exception as e:
                logging.error(e)
                raise e
            if not json_data:
                self.data = {}
            else:
                self.data = json.loads(json_data)
    #在需要存储数据的地方调用save方法#
    def save(self):
        json_data = json.dumps(self.data)
        try:
            self._request_handler.redis.setex("sess_%s" % self.session_id,
                                             SESSION_EXPIRES_SECONDS, json_data)
        except Exception as e:
            logging.error(e)
            raise e
    #清除redis中的session_id#
    def clear(self):
        try:
            self._request_handler.redis.delete("sess_%s" % self.session_id)
        except Exception as e:
            logging.error(e)
        self._request_handler.clear_cookie("session_id")
```

[代码参考链接](https://blog.csdn.net/pengxuan3507/article/details/80431492)

