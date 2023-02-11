# Aggregation 이란?

- Collection의 데이터를 변환하거나 분석하기 위해 사용하는 집계 프레임워크
- Aggregation은 Find 함수로 처리할 수 없는, SQL의 Group By와 Join 구문 같은 복잡한 데이터 분석 기능들을 제공한다.
- Aggregation Framework는 Pipeline 형태를 갖춘다.
- MongoDb 2.2 부터 제공되었고 이전에는 Map Reduce를 사용했다.

# RDB와의 비교
```
SELECT productName, SUM(quantity) AS sumQuantity  
FROM orders  
WHERE status = ‘urgent’  
GROUP BY productName;  
```
```
db.orders.aggregate([  
  { $match: { status: “urgent” },  
  {  
    $group: {  
      id: "$productName",  
      sumQuantity: { $sum: "$quantity" }  
    }  
  }  
]) 
```

# Aggregation Pipeline
![image](https://user-images.githubusercontent.com/46700734/218267363-95b42a2d-a641-45e2-8582-0b2ac7b48141.png)


