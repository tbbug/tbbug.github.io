---
layout: post
title: 微信用户信息rawData转数组
categories: [微信开发, solidity]
tags: [thinkphp, angular,webstrom, solidity,wechat]
status: publish
type: post
published: true
author: blackfox
permalink: /20180806/wechat-rawDatatostring.html
keyword: idea,webstrom,phpstorm solidity ,wechat
desc: 小程序getinfo获取用户信息微信用户信息rawData转数组
---
# 微信用户信息rawData转数组

### 小程序getinfo获取用户信息微信用户信息rawData转数组

```


//rawData转数组
public static function rawDatatoArray($rawData)
{

​    $newArray = [];
    if($rawData!='uninfo'){
        $rawData = str_replace('{', '', $rawData);
        $rawData = str_replace('}', '', $rawData);
        $url = explode('"avatarUrl":"', $rawData);
        $url = str_replace('"', '', $url[1]);
        $rawData = str_replace('"', '', $rawData);
        $rawData = explode(',', $rawData);

​        foreach ($rawData as $key => $v) {
            if (!empty($v)) {
                $key1 = explode(":", $v);
                $newArray[$key1[0]] = $key1[1];
            }

​        };
        $newArray['avatarUrl'] = $url;
    }else{

​        $newArray=array(
            'avatarUrl' =>'',
            'nickName' =>'uninfo'

​        );

​    }

​    return $newArray;
}
```

