## Tiktok crawler cluster for enterprise [中文](https://github.com/botsphp/douyin_crawler)

tiktok crawler is the data acquisition interface for tiktok which can 100% remove the watermark on tiktok videos without server or proxy IP.

Can craw for 10 millions per day.

#### 2019.12.20 add comment api
#### 2020.12.20 add tiktok interface which is compatible with douyin interfaces except the goods api
#### 2020.01.13 add douyin goods interface

## Core Functions and Advantages

1. With the current frequent upgrade of tiktok, there are more and more restrictions on the old version. The old signature algorithm would expire, can’t return any data, or often blocked, causing frequent changes of interfaces and codes and rise in the cost of proxy IP maintaining. 

2. The current plan is to scrape data with the latest distributed acquisition system. A background task is supported by multiple different IP protocols and signatures to ensure that data can return, breaking the bottleneck of single point system and lowering the cost.

3. Using simple interfaces, now the scraping can reach to tens of million times every day, highly efficient.

4. Cloud plan is adopted, so there no need for crawl server, proxy IP or upgrade.

#### Demo Site(Chinese)

> https://yundou.me/

#### service page

> https://service.yundou.me/

#### demo of sending task

```shell
curl -s -m 5 -d '{"token":"36ea7692e261cc32f593b2cd7eb7dc6c","type":"crawler_search_user","search":"面膜","num":20}' \
https://service.yundou.me/
```

#### When task is done, the client’s http callback api will receive a callback

> After the callback interface is successfully processed, a string of `{"code":200}` must return. 
> If the request to callback interface is over 10 seconds, then the response is deemed as failed(timeout), in that case it retries again only once.
> If callback reception is failed. A new task can be launched and data extraction task will be validated for several times. Once failed, there will be a new IP for the task. 
> One task can be tried for maximum 9 times and is deemed as failed if it lasts over 5 minutes. 
> The callback api is HTTP only, https not supported for now.


#### List of supported api

- crawler_search_user: Search via tiktok user ID (UID)
- crawler_search_video: Search video via keyword
- crawler_user_info: Return user’s detail information by UID
- crawler_user_following: Return user’s FOLLOWING information by UID
- crawler_user_follower: Return user’s FOLLOWER information by UID
- crawler_user_post: Return user’s POSTS information by UID
- crawler_user_favorite: Return user’s LIKES information by UID
- crawler_nearby_feed: Return USER and POSTS list according to the city
- crawler_comment_list: Return comment list by post ID
- crawler_search_goods: Search goods(Douyin Only)
- crawler_user_goods: Search goods by UID (Douyin Only)

#### list of acceptable parameter

```json
{
    "token": "",
    "num": 20,
    "type": "crawler_search_user",
    "uid": "85635793",
    "vid": "6763872129701124",
    "sec_uid": "MS4wLjABAAAA6FJbgV0BY17eGBY",
    "city_id": "510100",
    "search": "abcdefg",
    "task":"your_uniq_id",
    "result": []
}
```

> The parameters for different tasks are different. See detailed parameters bellow
> `token` is the allocated key after purchase. Please keep in mind to renew the payment
> `task` is a reserved field that only supports strings of up to 16 characters, which can be used to mark your unique task id.
> `result` is the result of data


#### RESPONSE

>
```json
{
    "code": 200
}
```

```json
{
    "code": 500,
    "msg": "excetion msg"
}
```

#### Details

> tiktok `"app":"tiktok"`
> douyin `"app":"douyin"` DEFAULT

```json
{
    ...
    "app":"tiktok"
    ...
}
```

```json
{
    "num": 20,
    "type": "crawler_search_user",
    "search": "abc12345678",
    "app": "tiktok",
}
```

```json
{
    "num": 20,
    "type": "crawler_search_video",
    "search": "abc12345678"
}
```

> `uid` and `sec_uid` required

```json
{
    "id": 0,
    "type": "crawler_user_info",
    "uid": "9338953804",
    "sec_uid": "MS4wLjABAAAAQ4xCNiRbRwIg"
}
```

> `uid` and `sec_uid` required

```json
{
    "id": 0,
    "num": 20,
    "type": "crawler_user_favorite",
    "uid": "632494600",
    "sec_uid": "MS4wLjABAAAAQ4xCNiRbRwIg"
}
```

> `uid` and `sec_uid` required

```json
{
    "id": 0,
    "num": 20,
    "type": "crawler_user_post",
    "uid": "632494600",
    "sec_uid": "MS4wLjABAAAAQ4xCNiRbRwIg"
}
```

> `vid` required

```json
{
    "id": 0,
    "num": 20,
    "type": "crawler_comment_list",
    "vid": "66082937525764932"
}
```

> `uid` and `sec_uid` required

```json
{
    "id": 0,
    "num": 20,
    "type": "crawler_user_follower",
    "uid": "16361944337",
    "sec_uid": "MS4wLjABAAAAQ4xCNiRbRwIg"
}
```

> `uid` and `sec_uid` required

```json
{
    "id": 0,
    "num": 20,
    "type": "crawler_user_following",
    "uid": "163619337",
    "sec_uid": "tWyVTUdvPOg90efQ7E"
}
```

> Must include `city_id` or `coordination`

```json
{
    "id": 0,
    "num": 20,
    "type": "crawler_nearby_feed",
    "city_id": "510900",
    "longitude": "105.389997",
    "latitude": "30.87346",
}

```

```json
{
    "num": 20,
    "type": "crawler_search_goods",
    "search": "toys"
}
```

> `uid` and `sec_uid` required

```json
{
    "id": 0,
    "num": 20,
    "type": "crawler_user_goods",
    "uid": "16361944337",
    "sec_uid": "MS4wLjABAAAAQ4xCNiRbRwIg"
}
```

#### Warning

1. This website is only for study and research.
2. Please abide by Chinese law, Commercial use is prohibited. 

#### Contacts us

1. wec.cloud@gmail.com
2. tg: +639288446666

