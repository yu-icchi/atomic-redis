# atomic-ioredis

MongoDB-Query like redis atomic update with ioredis adapter.

Luaスクリプトでアトミックに更新できるようにしている。

## extend-API

### findAndModify(key, query, update, options, callback)

Find and update a hashes or list.

|Name|Type|Default|Description|
|:---|:---|:------|:----------|
|key|string| |Redisのキー|
|query|object| |クエリオブジェクト|
|update|object| |更新用オブジェクト|
|options|object|null|options.new: boolean|
|callback|function| |コールバック関数|

#### Find Query

##### Comparison

- $eq
- $gt
- $gte
- $lt
- $lte
- $ne
- $in
- $nin

##### Logical

- $or
- $and
- $not
- $nor

##### Element

- $exists

##### Array

- $elemMatch
- $size

#### Update Query

##### Fields

- $inc
- $setOnInsert
- $set
- $unset
- $min
- $max

##### Array

- $addToSet
- $pop
- $pullAll
- $pull
- $pushAll
- $push

##### Modifiers

- $each
- $slice
- $sort

## Example

Queryに引っかかったモノだけ更新する

```javascript
var redis = require('atomic-ioredis');
var query = {
  id: 'test', // {$eq: 'test'}
  num: {$gte: 100}
};
var update = {
  $inc: {num: 1},
  $set: {name: 'test'}
};
var options = {
  new: true
};
redis.findAndModify('key', query, update, options, callback);
```
