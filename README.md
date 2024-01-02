# ![Dynamic JSON Badge](https://img.shields.io/badge/dynamic/json?url=http%3A%2F%2Fygo-card-db.7fyyuujdwn39.online%2Fapi%2Fv1%2Fcards%2Fen%2Fcids&query=1&label=Service%20Status)
# yugioh-card-database-service-document
 - 遊戲王卡片的資訊服務，資料是從konami的網站上爬下來的，所以有更新的話也會自動更新
 - 如果有問題的話也歡迎寄信給我internetms52@gmail.com

## 主要功能
 - 查詢該語系所有cid清單
 - 依照cid查詢卡片內容
 - 使用Elasticsearch Json Query DSL查詢卡片內容
 
 ### 支持語系
 - 英文(en)
 - 日文(jp)
 #### 語系信息應包含在路徑變量中,例如:http://ygo-card-db.7fyyuujdwn39.online/api/v1/cards/en/cids
 
### API Entrypoint

 #### 查詢該語系的所有卡片cid清單
 - method: GET 
 - http://ygo-card-db.7fyyuujdwn39.online/api/v1/cards/{locale}/cids
 #### 依照cid取得該語系的卡片資訊
 - method: GET 
 - http://ygo-card-db.7fyyuujdwn39.online/api/v1/cards/{locale}/{cid}
 #### 依照Elasticsearch Json Query DSL 查詢卡片內容
 - method: POST
 - http://ygo-card-db.7fyyuujdwn39.online/api/v1/cards/{locale}/elastic/json/dsl
 
 ### API 支持使用 [Elasticsearch Query DSL](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl.html) 作為查詢語句。
Elasticsearch Query DSL 是 Elasticsearch 提供的彈性 JSON 格式的查詢語法。它支持建構從簡單查詢到複雜邏輯的各種查詢。
例如：
```
{
  "query": {
    "bool": {
      "must": [
        { "match_phrase": { "enName": "Dark Magician" }},  
        { "term": { "level": 7 }}
      ]
    }
  }  
}
```
 #### 組合查詢字段
 ##### 文本字段型別可以使用模糊搜尋
 
| 字段型別  	    | 		名稱		           | 		描述				         |
|------------|------------------|------------------|
| 	TEXT		    | 	enName			       | 英文卡名(en限定)			    |
| 	TEXT		    | 	kanjiName		     | 日文漢字卡名(jp限定)		   |
| 	TEXT		    | 	kanaName		      | 日文假名卡名(jp限定)		   |
| 	TEXT		    | 	attributes		    | 屬性						         |
| 	INTEGER		 | 	level			        | 星數						         |
| 	INTEGER		      | 	rank			         | 超量階級					        |
| 	KEYWORD		      | 	cid				         | 卡片唯一號碼				       |
| 	INTEGER		      | 	atk				         | 攻擊力(部份為-浮動數值)	   |
| 	INTEGER		      | 	def				         | 防禦力(部份為-浮動數值)	   |
| 	KEYWORD	  | 	atkRemark				   | 攻擊力備註(-,?)	 |
| 	KEYWORD		 | 	defRemark				   | 防禦力備註(-,?)	      |
| 	TEXT		      | 	monsterTypes	   | 怪獸類型(怪獸卡專用)		    |
| 	TEXT		      | 	cardTypes		     | 卡片類型(非怪獸卡專用)	    |
| 	INTEGER		      | 	linkLevel		     | 連接等級					        |
| 	INTEGER		      | 	linkDirections	 | 連接方向					        |
| 	INTEGER		      | 	pendulumScale	  | 靈擺階級					        |
| 	TEXT		      | 	pendulumEffect	 | 靈擺效果					        |
| 	TEXT		      | 	cardText		      | 卡片效果					        |

## 程式更版記錄請見[wiki](https://github.com/internetms52/yugioh-card-database-service-document/wiki/History)

## 停電停機公告 UTC+8 2024/01/02 08:35  ~2024/01/02 13:00
