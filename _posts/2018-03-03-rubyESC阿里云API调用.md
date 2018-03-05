---
layout: post
title: "ruby_ESC阿里云API调用验证签名"
date: 2018-03-03
description: "ruby_ESC阿里云API调用验证签名"
tag: Ruby
--- 
### 官方API调用文档
[https://help.aliyun.com/document_detail/25492.html?spm=a2c4g.11186623.6.844.NytcL7](https://help.aliyun.com/document_detail/25492.html?spm=a2c4g.11186623.6.844.NytcL7)

### 签名机制计算

```
require 'cgi'
require 'json'
require 'base64'
require 'openssl'
require 'rest-client'
require 'securerandom'

class EscApi

  #ESC API 服务接入地址
  def self.base_url
    "https://ecs.aliyuncs.com/?"
  end
  
  #阿里云颁发给用户的访问服务所用的密钥 ID。
  def self.access_key_id
    "fQs*******"
  end

  #是用于加密签名字符串和服务器端验证签名字符串的密钥
  def self.access_key_secrete
    "Y1t*******"
  end

  #字符串构造，参数排序
  def self.generate_stander_string(params)
      str = ''
      keys = params.keys.sort
      keys.each do |key|
        str += "#{CGI.escape(key.to_s)}=#{CGI.escape(params[key.to_sym])}&"
      end
      str.gsub(/\&$/, '')
  end

  #当前时间戳 UTC
  def self.get_utc_timestamp
      Time.now.utc.strftime("%FT%TZ")
  end

  #唯一随机数，用于防止网络重放攻击。用户在不同请求间要使用不同的随机数值
  def self.get_nonce
    SecureRandom.uuid
  end

  #构造公共请求参数
  def self.create_params(params)
    rest_params = {
        AccessKeyId: access_key_id,
        Timestamp: get_utc_timestamp,
        SignatureMethod: 'HMAC-SHA1',
        SignatureVersion: '1.0',
        SignatureNonce: get_nonce,
        Format: "JSON",
        Version: "2014-05-26"
    }
    params.merge rest_params
  end

  #签名计算
  def self.get_signature(params)
    stander_string = generate_stander_string(params)
    construct_string = 'GET&' + CGI.escape('/') + '&' + CGI.escape(stander_string)
    digest = OpenSSL::Digest.new('sha1')
    key = access_key_secrete + '&'
    Base64.strict_encode64(OpenSSL::HMAC.digest(digest, key, construct_string))
  end

  #请求参数拼接
  def self.get_request_params(params)
    final_params = create_params(params)
    final_params.merge!(params)
    signature = get_signature(final_params)
    final_params.merge!({Signature: signature})
  end


  #发起请求
  def self.request(params)
    req_params = get_request_params(params)
    res = JSON.parse(RestClient.get(base_url,{params:req_params}))
  end
end
#查看区域
puts res = EscApi.request({Action:"DescribeRegions"})
```
