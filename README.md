# yugioh-card-database-service-document
yugioh-card-database-service-document

## 主要功能
 - 查詢該語系所有Cid清單
 - 依照cid查詢卡片內容
 - 使用Elasticsearch Json Query Dsl查詢卡片內容
 
 ### 支持語系
 - 英文(en)
 - 日文(jp)
 #### 語系信息應包含在路徑變量中,例如:http://36.229.109.58:8903/api/v1/cards/en/cids
 
### API Entrypoint

 #### 查詢該語系的所有卡片cid清單
 - method: GET 
 - http://36.229.109.58:8903/api/v1/cards/{locale}/cids
 #### 依照cid取得該語系的卡片資訊
 - method: GET 
 - http://36.229.109.58:8903/api/v1/cards/{locale}/{cid}
 #### 依照Elasticsearch Json Query DSL 查詢卡片內容
 - method: POST
 - http://36.229.109.58:8903/api/v1/cards/{locale}/elastic/json/dsl
 
 ### 本 API 支持使用 [Elasticsearch Query DSL](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl.html) 作為查詢語句。
Elasticsearch Query DSL 是 Elasticsearch 提供的彈性 JSON 格式的查詢語法。它支持構建從简單查詢到複雜邏輯的各種查詢。
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
 
| 字段型別  	| 		名稱		|		描述				|
| ------------- | ----------------- |---------------------------|
|	文本		| 	enName			| 英文卡名(en限定)			|
|	文本		| 	kanjiName		| 日文漢字卡名(jp限定)		|
|	文本		| 	kanaName		| 日文假名卡名(jp限定)		|
|	文本		| 	attributes		| 屬性						|
|	數字		| 	level			| 星數						|
|	數字		| 	rank			| 超量階級					|
|	字串		| 	cid				| 卡片唯一號碼				|
|	文本		| 	atk				| 攻擊力(部份為-浮動數值)	|
|	文本		| 	def				| 防禦力(部份為-浮動數值)	|
|	文本		| 	monsterTypes	| 怪獸類型(怪獸卡專用)		|
|	文本		| 	cardTypes		| 卡片類型(非怪獸卡專用)	|
|	數字		| 	linkLevel		| 連接等級					|
|	數字		| 	linkDirections	| 連接方向					|
|	數字		| 	pendulumScale	| 靈擺階級					|
|	文本		| 	pendulumEffect	| 靈擺效果					|
|	文本		| 	cardText		| 卡片效果					|
