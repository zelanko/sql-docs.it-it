---
title: Query dei dati spaziali per Nearest Neighbor | Microsoft Docs
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 7af4ad5d-484e-45b4-aa16-83c33b358bb6
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 099771b9900d4c39de40b176cde5c92fa0c95462
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/22/2019
ms.locfileid: "66014107"
---
# <a name="query-spatial-data-for-nearest-neighbor"></a>Query dei dati spaziali per Nearest Neighbor
  La query Nearest Neighbor è una query comune utilizzata con dati spaziali. Le query Nearest Neighbor vengono utilizzate per trovare gli oggetti spaziali più vicini a un oggetto spaziale specifico. Un localizzatore di archivio per un sito Web, ad esempio, deve spesso trovare i percorsi di archivio più vicini alla posizione di un cliente.  
  
 Una query Nearest Neighbor può essere scritta in una varietà di formati di query validi, ma per l'utilizzo di un indice spaziale è necessario utilizzare la sintassi seguente.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
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
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], per eseguire una query Nearest Neighbor nelle colonne di dati spaziali, vengono utilizzate le clausole `TOP` e `ORDER BY`. La clausola `ORDER BY` contiene una chiamata al metodo `STDistance()` per il tipo di dati della colonna spaziale. La clausola `TOP` indica il numero di oggetti da restituire per la query.  
  
 Per utilizzare un indice spaziale in una query Nearest Neighbor, è necessario soddisfare i requisiti seguenti:  
  
1.  In una delle colonne spaziali deve essere presente un indice spaziale e tale colonna deve essere utilizzata dal metodo `STDistance()` nelle clausole `WHERE` e `ORDER BY`.  
  
2.  La clausola `TOP` non può contenere un'istruzione `PERCENT`.  
  
3.  La clausola `WHERE` deve contenere un metodo `STDistance()`.  
  
4.  Se nella clausola `WHERE` sono presenti più predicati, il predicato che contiene il metodo `STDistance()` deve essere connesso mediante una congiunzione `AND` ad altri predicati. Il metodo `STDistance()` non può trovarsi in una parte facoltativa della clausola `WHERE`.  
  
5.  La prima espressione nella clausola `ORDER BY` deve utilizzare il metodo `STDistance()`.  
  
6.  L'ordinamento per la prima espressione `STDistance()` nella clausola `ORDER BY` deve essere `ASC`.  
  
7.  Devono essere filtrate tutte le righe per le quali `STDistance` restituisce `NULL`.  
  
> [!WARNING]  
>  I metodi che accettano tipi di dati `geography` o `geometry` come argomenti restituiranno `NULL` se gli identificatori SRID non sono gli stessi per i tipi.  
  
 Per gli indici utilizzati nelle query Nearest Neighbor è consigliabile utilizzare i nuovi schemi a mosaico di indice spaziale. Per altre informazioni sugli schemi a mosaico di indice spaziale, vedere [Dati spaziali &#40;SQL Server&#41;](spatial-data-sql-server.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio di codice seguente viene illustrata una query Nearest Neighbor nella quale può essere utilizzato un indice spaziale. Nell'esempio viene utilizzata la tabella `Person.Address` del database `AdventureWorks2012` .  
  
```  
USE AdventureWorks2012  
GO  
DECLARE @g geography = 'POINT(-121.626 47.8315)';  
SELECT TOP(7) SpatialLocation.ToString(), City FROM Person.Address  
WHERE SpatialLocation.STDistance(@g) IS NOT NULL  
ORDER BY SpatialLocation.STDistance(@g);  
  
```  
  
 Creare un indice spaziale nella colonna SpatialLocation per vedere in che modo viene utilizzato un indice spaziale in una query Nearest Neighbor. Per ulteriori informazioni sulla creazione di indici spaziali, vedere [Create, Modify, and Drop Spatial Indexes](create-modify-and-drop-spatial-indexes.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio di codice seguente viene illustrata una query Nearest Neighbor nella quale non può essere utilizzato un indice spaziale.  
  
```  
USE AdventureWorks2012  
GO  
DECLARE @g geography = 'POINT(-121.626 47.8315)';  
SELECT TOP(7) SpatialLocation.ToString(), City FROM Person.Address  
ORDER BY SpatialLocation.STDistance(@g);  
  
```  
  
 Nella query manca una clausola `WHERE` che utilizza `STDistance()` in un formato specificato nella sezione relativa alla sintassi, pertanto nella query non può essere utilizzato un indice spaziale.  
  
## <a name="see-also"></a>Vedere anche  
 [Dati spaziali &#40;SQL Server&#41;](spatial-data-sql-server.md)  
  
  
