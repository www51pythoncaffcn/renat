# renat
#!/usr/bin/env python3
# -*- coding: utf-8-*-

import time
import hmac
import hashlib
import base64
import requests
import dingtalk

import json

import urllib
from urllib import parse

def jinshan():
    
    
    jinurl='http://open.iciba.com/dsapi/'
    
    res=requests.get(jinurl).text
    
    respond=json.loads(res)['note']
    
    return respond
    


def At():


    
 # 时间戳

    timestamp = str (round (time.time () * 1000))
    # 钉钉加签
    secret = 'SECbb31344613f5730dad068081f967e65390c2368f230f5d4c357dd844ea50d193'
    secret_enc = secret.encode ('utf-8')
    string_to_sign = '{}\n{}'.format (timestamp, secret)
    string_to_sign_enc = string_to_sign.encode ('utf-8')
    hmac_code = hmac.new (secret_enc, string_to_sign_enc, digestmod=hashlib.sha256).digest ()
    sign = urllib.parse.quote_plus (base64.b64encode (hmac_code))
    print (timestamp)
    print (sign)
    # 钉钉机器人中的Webhook+sign+timestamp
    url = 'https://oapi.dingtalk.com/robot/send?access_token=849a0e39e5e07f7d176ebd7b27ca8a75ae7d550865ea5179b5be2fb57206f131&timestamp={0}&sign={1}'.format (timestamp, sign)
    
    headers={"Content-Type":"application/json;charset=utf-8"}
    
    moble=['18010050296','18010050296','18010050296','18010050296','18813127541']
    
    localtime = time.localtime(time.time())
    
    wday=localtime.tm_wday

    year=str(localtime.tm_year)
    month=str(localtime.tm_mon)
    day=str(localtime.tm_mday)

    ymd=year+"-"+month+"-"+day
    
    ciyu=jinshan()
    
    if(wday==5):
    
       print("今天周末,周末愉快")
        
    elif(wday==6):
    
       print("今天周末,周末愉快")
    
    elif(wday==0):
        
        amobie=moble[0]
        
        data1={

            "at": {
                "atMobiles":[amobie],
                "atUserIds":[],
                "isAtAll": False
            },
            "text": {
                "content":"娜姐好,今天是："+ymd+","+"周一"+","+"美好的一周开始了，但不要太累哈"+"\n"+"'"+ciyu+"'"+"(来自金山每日一句)"
            },
            "msgtype":"text"
        }
        
        
        data=json.dumps(data1)

        response=requests.post(url,data=data,headers=headers)


        print(response.text)


    elif(wday==1):
    
        amobie=moble[1]
        
        data1={

        "at": {
            "atMobiles":[amobie],
            "atUserIds":[],
            "isAtAll": False
        },
        "text": {
            "content":"利姐好,今天是："+ymd+","+"周二"+","+"已经上班一天了，注意休息"+"\n"+"'"+ciyu+"'"+"(来自金山每日一句)"
        },
        "msgtype":"text"
        }
        
        
        data=json.dumps(data1)

        response=requests.post(url,data=data,headers=headers)

        print(response.text)
        
        
        
    elif(wday==2):
    
        amobie=moble[2]
        
        data1={

        "at": {
            "atMobiles":[amobie],
            "atUserIds":[],
            "isAtAll": False
        },
        "text": {
            "content":"鹏鹏好,今天是："+ymd+","+"周三"+","+"今天不美好，啥时候找对象啊！"+"\n"+"'"+ciyu+"'"+"(来自金山每日一句)"
        },
        "msgtype":"text"
        }


        data=json.dumps(data1)


        response=requests.post(url,data=data,headers=headers)


        print(response.text)
        
    elif(wday==3):
    
        amobie=moble[3]
        
        data1={

        "at": {
            "atMobiles":[amobie],
            "atUserIds":[],
            "isAtAll": False
        },
        "text": {
            "content":"帅帅好,今天是："+ymd+","+"周四"+","+"马上周末了，太棒了"+"\n"+"'"+ciyu+"'"+"(来自金山每日一句)"
        },
        "msgtype":"text"
        }


        data=json.dumps(data1)



        response=requests.post(url,data=data,headers=headers)


        print(response.text)
        
    else :
    
        amobie=moble[4]
        
        data1={

        "at": {
            "atMobiles":[amobie],
            "atUserIds":[],
            "isAtAll": False
        },
        "text": {
            "content":"樊舒老师好,今天是："+ymd+","+"周五"+","+"这周回家吗"+"\n"+"'"+ciyu+"'"+"(来自金山每日一句)"
        },
        "msgtype":"text"
        }


        data=json.dumps(data1)



        response=requests.post(url,data=data,headers=headers)


        print(response.text)
        
     
        
    
    

if __name__ == '__main__':
    # 程序运行时调用方法
    At()
