---
title: ORDER BY(Entity SQL)
ms.date: 03/30/2017
ms.assetid: c0b61572-ecee-41eb-9d7f-74132ec8a26c
ms.openlocfilehash: 2010ef9d6fe37e65824cac877074453db1b789db
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72319441"
---
# <a name="order-by-entity-sql"></a>ORDER BY(Entity SQL)
SELECT 문에서 반환되는 개체에 적용하는 정렬 순서를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
[ ORDER BY   
   {  
      order_by_expression [SKIP n] [LIMIT n]  
      [ COLLATE collation_name ]  
      [ ASC | DESC ]  
   }  
   [ ,…n ]   
]  
```  
  
## <a name="arguments"></a>인수  
 `order_by_expression`  
 정렬 기준이 될 속성을 지정하는 유효한 쿼리 식입니다. 여러 정렬 식을 지정할 수 있습니다. ORDER BY 절에서 정렬 식의 시퀀스에 따라 정렬된 결과 집합의 구조가 정의됩니다.  
  
 COLLATE {collation_name}  
 `collation_name`에 지정된 데이터 정렬에 따라 ORDER BY 연산을 수행해야 함을 지정합니다. COLLATE는 문자열 식에만 적용됩니다.  
  
 ASC  
 지정된 속성에서 값이 오름차순으로, 즉 가장 작은 값에서 가장 큰 값으로 정렬되도록 지정합니다. 기본값입니다.  
  
 DESC  
 지정된 속성에서 값이 내림차순으로, 즉 가장 큰 값에서 가장 작은 값으로 정렬되도록 지정합니다.  
  
 LIMIT `n`  
 처음 `n` 개 항목만 선택됩니다.  
  
 SKIP `n`  
 처음 `n` 개 항목을 건너뜁니다.  
  
## <a name="remarks"></a>주의  
 ORDER BY 절은 SELECT 절의 결과에 논리적으로 적용됩니다. ORDER BY 절은 별칭을 사용하여 선택 목록 내 항목을 참조할 수 있습니다. ORDER BY 절은 현재 범위 내에 있는 다른 변수도 참조할 수 있습니다. 하지만, DISTINCT 한정자를 사용하여 SELECT 절이 지정된 경우 ORDER BY 절은 SELECT 절의 별칭만 참조할 수 있습니다.  
  
 `SELECT c AS c1 FROM cs AS c ORDER BY c1.e1, c.e2`  
  
 ORDER BY 절의 모든 식은 같지 않음 정렬(예: 보다 작음, 보다 큼)을 비교할 수 있는 형식으로 계산되어야 합니다. 이런 형식은 일반적으로 숫자, 문자열, 날짜와 같은 스칼라 기본 형식입니다. 비교 가능한 형식의 RowType도 순서를 비교할 수 있습니다.  
  
 최상위 프로젝션에 대해서가 아니라 정렬된 집합에 대해 코드가 반복되는 경우 출력에 순서가 유지되지 않을 수 있습니다.  

다음 샘플에서는 순서가 유지 되도록 보장 됩니다.

```sql  
SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName  
```  

다음 쿼리에서 중첩 쿼리의 순서는 무시 됩니다.  

```sql  
SELECT C2.FirstName, C2.LastName  
    FROM (SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName) as C2  
```  
  
 정렬된 UNION, UNION ALL, EXCEPT 또는 INTERSECT 연산을 얻으려면 다음 패턴을 사용하세요.  
  
```sql  
SELECT ...  
FROM ( UNION/EXCEPT/INTERSECT operation )  
ORDER BY ...  
```  
  
## <a name="restricted-keywords"></a>제한된 키워드  
 다음 키워드를 `ORDER BY` 절에서 사용할 때는 따옴표로 묶어야 합니다.  
  
- CROSS  
  
- FULL  
  
- KEY  
  
- LEFT  
  
- ORDER  
  
- OUTER  
  
- RIGHT  
  
- ROW  
  
- VALUE  
  
## <a name="ordering-nested-queries"></a>중첩 쿼리 순서  
 Entity Framework에서 중첩된 식은 쿼리 내 임의의 위치에 올 수 있습니다. 중첩 쿼리의 순서는 유지되지 않습니다.  

다음 쿼리는 성을 기준으로 결과를 정렬 합니다.  

```sql  
SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName  
```  

다음 쿼리에서 중첩 쿼리의 순서는 무시 됩니다.  

```sql  
SELECT C2.FirstName, C2.LastName  
    FROM (SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName) as C2  
```  
  
## <a name="example"></a>예제  
 다음 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 쿼리는 ORDER BY 연산자를 사용하여 SELECT 문에서 반환되는 개체에 적용하는 정렬 순서를 지정합니다. 쿼리는 AdventureWorks Sales 모델을 기반으로 합니다. 이 쿼리를 컴파일하고 실행하려면 다음 단계를 수행하세요.  
  
1. [How to: Execute a Query that Returns StructuralType Results](../how-to-execute-a-query-that-returns-structuraltype-results.md)의 절차를 따릅니다.  
  
2. 다음 쿼리를 `ExecuteStructuralTypeQuery` 메서드에 인수로 전달합니다.  
  
 [!code-sql[DP EntityServices Concepts#ORDERBY](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#orderby)]  
  
## <a name="see-also"></a>참조

- [쿼리 식](query-expressions-entity-sql.md)
- [엔터티 SQL 참조](entity-sql-reference.md)
- [SKIP](skip-entity-sql.md)
- [LIMIT](limit-entity-sql.md)
- [TOP](top-entity-sql.md)
