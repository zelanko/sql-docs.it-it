---
title: Query dei dati spaziali per Nearest Neighbor | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 7af4ad5d-484e-45b4-aa16-83c33b358bb6
author: MladjoA
ms.author: mlandzic
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 58a0131c84a1a257917a17238be773a8533d2794
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/20/2019
ms.locfileid: "65939227"
---
# <a name="query-spatial-data-for-nearest-neighbor"></a>Query dei dati spaziali per Nearest Neighbor
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  La query Nearest Neighbor è una query comune utilizzata con dati spaziali. Le query Nearest Neighbor vengono utilizzate per trovare gli oggetti spaziali più vicini a un oggetto spaziale specifico. Un localizzatore di archivio per un sito Web, ad esempio, deve spesso trovare i percorsi di archivio più vicini alla posizione di un cliente.  
  
 Una query Nearest Neighbor può essere scritta in una varietà di formati di query validi, ma per l'utilizzo di un indice spaziale è necessario utilizzare la sintassi seguente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
SELECT TOP ( number )  
        [ WITH TIES ]  
        [ * | expression ]   
        [, ...]  
    FROM spatial_table_reference, ...   
        [ WITH   
            (   
                [ INDEX ( index_ref ) ]   
                [ , SPATIAL_WINDOW_MAX_CELLS = <value>]   
                [ ,... ]   
            )   
        ]  
    WHERE   
        column_ref.STDistance ( @spatial_ object )   
            {   
                [ IS NOT NULL ] | [ < const ] | [ > const ]   
                | [ <= const ] | [ >= const ] | [ <> const ] ]   
            }  
            [ AND { other_predicate } ]   
    }  
    ORDER BY column_ref.STDistance ( @spatial_ object ) [ ,...n ]  
[ ; ]  
  
```  
  
## <a name="nearest-neighbor-query-and-spatial-indexes"></a>Query Nearest Neighbor e indici spaziali  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]vengono usate le clausole **TOP** e **ORDER BY** per eseguire una query Nearest Neighbor nelle colonne di dati spaziali. La clausola **ORDER BY** contiene una chiamata al metodo `STDistance()` per il tipo di dati della colonna spaziale. La clausola **TOP** indica il numero di oggetti da restituire per la query.  
  
 Per utilizzare un indice spaziale in una query Nearest Neighbor, è necessario soddisfare i requisiti seguenti:  
  
1.  In una delle colonne spaziali deve essere presente un indice spaziale e tale colonna deve essere usata dal metodo `STDistance()` nelle clausole **WHERE** e **ORDER BY** .  
  
2.  La clausola **TOP** non può contenere un'istruzione **PERCENT** .  
  
3.  La clausola **WHERE** deve contenere un metodo `STDistance()` .  
  
4.  Se nella clausola **WHERE** sono presenti più predicati, il predicato che contiene il metodo `STDistance()` deve essere connesso con una congiunzione **AND** ad altri predicati. Il metodo `STDistance()` non può trovarsi in una parte facoltativa della clausola **WHERE** .  
  
5.  La prima espressione nella clausola **ORDER BY** deve usare il metodo `STDistance()` .  
  
6.  L'ordinamento per la prima espressione `STDistance()` nella clausola **ORDER BY** deve essere **ASC**.  
  
7.  Devono essere filtrate tutte le righe per le quali `STDistance` restituisce **NULL** .  
  
> [!WARNING]  
>  I metodi che accettano tipi di dati **geography** o **geometry** come argomenti restituiranno **NULL** se gli identificatori SRID non sono gli stessi per i tipi.  
  
 Per gli indici utilizzati nelle query Nearest Neighbor è consigliabile utilizzare i nuovi schemi a mosaico di indice spaziale. Per altre informazioni sugli schemi a mosaico di indice spaziale, vedere [Dati spaziali &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio di codice seguente viene illustrata una query Nearest Neighbor nella quale può essere utilizzato un indice spaziale. Nell'esempio viene utilizzata la tabella `Person.Address` del database `AdventureWorks2016` .  
  
```sql  
USE AdventureWorks2016  
GO  
DECLARE @g geography = 'POINT(-121.626 47.8315)';  
SELECT TOP(7) SpatialLocation.ToString(), City FROM Person.Address  
WHERE SpatialLocation.STDistance(@g) IS NOT NULL  
ORDER BY SpatialLocation.STDistance(@g);  
```  
  
 Creare un indice spaziale nella colonna SpatialLocation per vedere in che modo viene utilizzato un indice spaziale in una query Nearest Neighbor. Per ulteriori informazioni sulla creazione di indici spaziali, vedere [Create, Modify, and Drop Spatial Indexes](../../relational-databases/spatial/create-modify-and-drop-spatial-indexes.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio di codice seguente viene illustrata una query Nearest Neighbor nella quale non può essere utilizzato un indice spaziale.  
  
```sql  
USE AdventureWorks2016  
GO  
DECLARE @g geography = 'POINT(-121.626 47.8315)';  
SELECT TOP(7) SpatialLocation.ToString(), City FROM Person.Address  
ORDER BY SpatialLocation.STDistance(@g);  
```  
  
 Nella query manca una clausola **WHERE** che usa `STDistance()` in un formato specificato nella sezione relativa alla sintassi, quindi la query non può usare un indice spaziale.  
  
## <a name="see-also"></a>Vedere anche  
 [Dati spaziali &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
