---
title: La modifica dei dati di tipo definito dall'utente | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- CAST function
- data deletions [CLR integration]
- data insertions [CLR integration]
- CONVERT function
- data updates [CLR integration]
- comparing data
- updating data [CLR integration]
- removing data
- IsByteOrdered property
- variables [CLR integration]
- data manipulation [CLR integration]
- user-defined types [CLR integration], data manipulation
- deleting data
- UDTs [CLR integration], data manipulation
- invoking UDT methods
- inserting data
ms.assetid: 51b1a5f2-7591-4e11-bfe2-d88e0836403f
author: rothja
ms.author: jroth
ms.openlocfilehash: 53471adf085fbe9a046d28fa09ce10a46953eae6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028176"
---
# <a name="working-with-user-defined-types---manipulating-udt-data"></a>Uso di tipi definiti dall'utente (UDT) - Modifica di dati UDT
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[tsql](../../includes/tsql-md.md)] non fornisce una sintassi specifica per l'istruzione INSERT, UPDATE o DELETE quando si modificano i dati nelle colonne con tipo definito dall'utente (UDT). Le funzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] CAST o CONVERT vengono utilizzate per eseguire il cast dei tipi di dati nativi al tipo UDT.  
  
## <a name="inserting-data-in-a-udt-column"></a>Inserimento di dati in una colonna con tipo definito dall'utente  
 Quanto segue [!INCLUDE[tsql](../../includes/tsql-md.md)] consentono di inserire tre righe di dati di esempio nel **punti** tabella. Il **punto** tipo di dati è costituita da X e Y integer valori che vengono esposti come proprietà del tipo in questione. È necessario utilizzare la funzione CAST o CONVERT per eseguire il cast di valori delimitati da virgole valori X e Y per il **punto** tipo. Le prime due istruzioni utilizzano la funzione CONVERT per convertire un valore stringa per il **punto** tipo e la terza istruzione utilizza la funzione CAST:  
  
```  
INSERT INTO dbo.Points (PointValue) VALUES (CONVERT(Point, '3,4'));  
INSERT INTO dbo.Points (PointValue) VALUES (CONVERT(Point, '1,5'));  
INSERT INTO dbo.Points (PointValue) VALUES (CAST ('1,99' AS Point));  
```  
  
## <a name="selecting-data"></a>Selezione dei dati  
 L'istruzione SELECT seguente consente di selezionare il valore binario del tipo definito dall'utente.  
  
```  
SELECT ID, PointValue FROM dbo.Points  
```  
  
 Per visualizzare l'output visualizzato in un formato leggibile, chiamare il **ToString** metodo per il **punto** tipo definito dall'utente, che converte il valore nella relativa rappresentazione di stringa.  
  
```  
SELECT ID, PointValue.ToString() AS PointValue   
FROM dbo.Points;  
```  
  
 Vengono prodotti i risultati seguenti:  
  
```  
ID PointValue  
-- ----------  
 1 3,4  
 2 1,5  
 3 1,99  
```  
  
 Per ottenere gli stessi risultati, è anche possibile utilizzare le funzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] CAST e CONVERT.  
  
```  
SELECT ID, CAST(PointValue AS varchar)   
FROM dbo.Points;  
  
SELECT ID, CONVERT(varchar, PointValue)   
FROM dbo.Points;  
```  
  
 Il **punto** UDT espone le coordinate X e Y come proprietà che è quindi possibile selezionare singolarmente. L'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente consente di selezionare le coordinate X e Y separatamente:  
  
```  
SELECT ID, PointValue.X AS xVal, PointValue.Y AS yVal   
FROM dbo.Points;  
```  
  
 Le proprietà X e Y restituiscono un valore integer visualizzato nel set di risultati.  
  
```  
ID xVal yVal  
-- ---- ----  
 1    3    4  
 2    1    5  
 3    1   99  
```  
  
## <a name="working-with-variables"></a>Gestione delle variabili  
 È possibile utilizzare le variabili specificando l'istruzione DECLARE per assegnare una variabile a un tipo definito dall'utente. Le istruzioni seguenti assegnano un valore utilizzando il [!INCLUDE[tsql](../../includes/tsql-md.md)] impostare l'istruzione e visualizzare i risultati, chiamare l'UDT **ToString** metodo sulla variabile:  
  
```  
DECLARE @PointValue Point;  
SET @PointValue = (SELECT PointValue FROM dbo.Points  
    WHERE ID = 2);  
SELECT @PointValue.ToString() AS PointValue;  
```  
  
 Nel set di risultati viene visualizzato il valore della variabile:  
  
```  
PointValue  
----------  
-1,5  
```  
  
 Le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] seguenti consentono di ottenere lo stesso risultato utilizzando SELECT anziché SET per l'assegnazione delle variabili:  
  
```  
DECLARE @PointValue Point;  
SELECT @PointValue = PointValue FROM dbo.Points  
    WHERE ID = 2;  
SELECT @PointValue.ToString() AS PointValue;  
```  
  
 La differenza tra l'utilizzo di SELECT e di SET per l'assegnazione delle variabili sta nel fatto che SELECT consente di assegnare più variabili in un'istruzione SELECT, mentre la sintassi di SET richiede che ogni assegnazione di variabile contenga la relativa istruzione SET.  
  
## <a name="comparing-data"></a>Confronto dei dati  
 È possibile usare gli operatori di confronto per confrontare i valori di tipo definito dall'utente se è stato impostato il **IsByteOrdered** proprietà **true** quando si definisce la classe. Per altre informazioni, vedere [creazione di un tipo definito dall'utente](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md).  
  
```  
SELECT ID, PointValue.ToString() AS Points   
FROM dbo.Points  
WHERE PointValue > CONVERT(Point, '2,2');  
```  
  
 È possibile confrontare valori interni dell'UDT indipendentemente i **IsByteOrdered** impostazione se i valori stessi sono confrontabili. L'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente consente di selezionare le righe in cui X è maggiore di Y:  
  
```  
SELECT ID, PointValue.ToString() AS PointValue   
FROM dbo.Points  
WHERE PointValue.X < PointValue.Y;  
```  
  
 È anche possibile utilizzare gli operatori di confronto con le variabili, come mostrato in questa query che esegue la ricerca di un valore PointValue corrispondente.  
  
```  
DECLARE @ComparePoint Point;  
SET @ComparePoint = CONVERT(Point, '3,4');  
SELECT ID, PointValue.ToString() AS MatchingPoint   
FROM dbo.Points  
WHERE PointValue = @ComparePoint;  
```  
  
## <a name="invoking-udt-methods"></a>Chiamata dei metodi UDT  
 È anche possibile richiamare i metodi definiti nel tipo definito dall'utente in [!INCLUDE[tsql](../../includes/tsql-md.md)]. Il **punto** classe contiene tre metodi **distanza**, **DistanceFrom**, e **DistanceFromXY**. Per i listati di codice che definisce questi tre metodi, vedere [codifica di tipi](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
 Quanto segue [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione chiama il **PointValue. Distance** metodo:  
  
```  
SELECT ID, PointValue.X AS [Point.X],   
    PointValue.Y AS [Point.Y],  
    PointValue.Distance() AS DistanceFromZero   
FROM dbo.Points;  
```  
  
 I risultati vengono visualizzati nei **distanza** colonna:  
  
```  
ID X  Y  Distance  
-- -- -- ----------------  
 1  3  4                5  
 2  1  5 5.09901951359278  
 3  1 99 99.0050503762308  
```  
  
 Il **DistanceFrom** metodo accetta un argomento di **puntare** tipo di dati e Visualizza la distanza dal punto specificato a PointValue:  
  
```  
SELECT ID, PointValue.ToString() AS Pnt,  
   PointValue.DistanceFrom(CONVERT(Point, '1,99')) AS DistanceFromPoint  
FROM dbo.Points;  
```  
  
 I risultati vengono visualizzati i risultati del **DistanceFrom** metodo per ogni riga nella tabella:  
  
```  
ID Pnt DistanceFromPoint  
-- --- -----------------  
 1 3,4  95.0210502993942  
 2 1,5                94  
 3 1,9                90  
```  
  
 Il **DistanceFromXY** metodo accetta i singoli punti come argomenti:  
  
```  
SELECT ID, PointValue.X as X, PointValue.Y as Y,   
PointValue.DistanceFromXY(1, 99) AS DistanceFromXY   
FROM dbo.Points  
```  
  
 Il set di risultati è identico il **DistanceFrom** (metodo).  
  
## <a name="updating-data-in-a-udt-column"></a>Aggiornamento dei dati in una colonna con tipo definito dall'utente  
 Per aggiornare i dati in una colonna con tipo definito dall'utente, utilizzare l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] UPDATE. Per aggiornare lo stato dell'oggetto è anche possibile utilizzare un metodo del tipo definito dall'utente. L'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente consente di aggiornare una singola riga nella tabella:  
  
```  
UPDATE dbo.Points  
SET PointValue = CAST('1,88' AS Point)  
WHERE ID = 3  
```  
  
 È anche possibile aggiornare gli elementi UDT separatamente. L'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente consente di aggiornare solo la coordinata Y:  
  
```  
UPDATE dbo.Points  
SET PointValue.Y = 99  
WHERE ID = 3  
```  
  
 Se il tipo definito dall'utente è stato definito con l'ordine dei byte impostato a **true**, [!INCLUDE[tsql](../../includes/tsql-md.md)] può valutare la colonna di tipo definito dall'utente in una clausola WHERE.  
  
```  
UPDATE dbo.Points  
SET PointValue = '4,5'  
WHERE PointValue = '3,4';  
```  
  
### <a name="updating-limitations"></a>Limitazioni relative all'aggiornamento  
 Non è possibile aggiornare più proprietà contemporaneamente utilizzando [!INCLUDE[tsql](../../includes/tsql-md.md)]. L'istruzione UPDATE seguente, ad esempio, ha esito negativo e restituisce un errore perché non è possibile utilizzare due volte lo stesso nome di colonna in un'istruzione UDATE.  
  
```  
UPDATE dbo.Points  
SET PointValue.X = 5, PointValue.Y = 99  
WHERE ID = 3  
```  
  
 Per aggiornare ogni punto singolarmente, è necessario creare un metodo mutatore nell'assembly del tipo definito dall'utente Point. È quindi possibile richiamare il metodo mutatore per aggiornare l'oggetto in un'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] UPDATE, come illustrato di seguito:  
  
```  
UPDATE dbo.Points  
SET PointValue.SetXY(5, 99)  
WHERE ID = 3  
```  
  
## <a name="deleting-data-in-a-udt-column"></a>Eliminazione di dati in una colonna con tipo definito dall'utente  
 Per eliminare dati in un tipo definito dall'utente, utilizzare l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] DELETE. L'istruzione seguente consente di eliminare tutte le righe della tabella che corrispondono ai criteri specificati nella clausola WHERE. Se si omette la clausola WHERE in un'istruzione DELETE, verranno eliminate tutte le righe della tabella.  
  
```  
DELETE FROM dbo.Points  
WHERE PointValue = CAST('1,99' AS Point)  
```  
  
 Utilizzare l'istruzione UPDATE se si desidera rimuovere i valori in una colonna con tipo definito dall'utente, senza tuttavia modificare i valori di altre righe. In questo esempio PointValue viene impostato su Null.  
  
```  
UPDATE dbo.Points  
SET PointValue = null  
WHERE ID = 2  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Uso di tipi definiti dall'utente in SQL Server](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md)  
  
  
