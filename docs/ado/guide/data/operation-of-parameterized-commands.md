---
title: Funzionamento dei comandi con parametri | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], parameterized commands
- parameterized commands [ADO]
ms.assetid: 4fae0d54-83b6-4ead-99cc-bcf532daa121
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: faa4d4887079064ac6ccbe9536ac6c36fe8b9f79
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52516987"
---
# <a name="operation-of-parameterized-commands"></a>Funzionamento dei comandi con parametri
Se si lavora con un elemento figlio di grandi dimensioni **Recordset**, in particolare rispetto alle dimensioni dell'elemento padre **Recordset**, ma è necessario accedere solo ad alcuni capitoli figlio, può risultare più efficiente usare un' comando con parametri.  
  
 Oggetto *senza parametri comando* recupera intera padre e figlio **recordset**, aggiunge una colonna a capitoli a padre e quindi assegna un riferimento al capitolo figlio correlati per ogni riga padre .  
  
 Oggetto *comando con parametri* recupera l'elemento padre intera **Recordset**, ma recupera solo il capitolo **Recordset** quando si accede alla colonna del capitolo. Questa differenza nella strategia di recupero può produrre vantaggi significativi delle prestazioni.  
  
 Ad esempio, è possibile specificare quanto segue:  
  
```  
SHAPE {SELECT * FROM customer}   
   APPEND ({SELECT * FROM orders WHERE cust_id = ?}   
   RELATE cust_id TO PARAMETER 0)  
```  
  
 Le tabelle padre e figlio di un nome di colonna, cust_id *.* Il *comando figlio* dispone di un "?" segnaposto, a cui fa riferimento la clausola RELATE (vale a dire, "... PARAMETRO 0").  
  
> [!NOTE]
>  La clausola parametro riguarda esclusivamente la sintassi dei comandi di forma. Non è associato uno ADO [parametri](../../../ado/reference/ado-api/parameter-object.md) oggetto o il [parametri](../../../ado/reference/ado-api/parameters-collection-ado.md) raccolta.  
  
 Quando viene eseguito il comando di forma con parametri, si verifica quanto segue:  
  
1.  Il *comando padre* non viene eseguita e restituisce un elemento padre **Recordset** dalla tabella Customers.  
  
2.  Una colonna del capitolo viene aggiunto all'elemento padre **Recordset**.  
  
3.  Quando si accede la colonna a capitoli di una riga padre, il *comando figlio* viene eseguita usando il valore di Customer. cust_id come il valore del parametro.  
  
4.  Tutte le righe nel set di righe del provider dati creato nel passaggio 3 vengono usate per popolare l'elemento figlio **Recordset**. In questo esempio, ovvero tutte le righe della tabella di ordini in cui il cust_id è uguale al valore di Customer. cust_id. Per impostazione predefinita, l'elemento figlio **Recordset**s verrà memorizzata nel client fino a tutti i riferimenti all'elemento padre **Recordset** vengono rilasciati. Per modificare questo comportamento, impostare il **Recordset** [proprietà dinamica](../../../ado/reference/ado-api/ado-dynamic-property-index.md) **righe figlio Cache** al **False**.  
  
5.  Un riferimento alle righe figlio recuperati (vale a dire, il capitolo dell'elemento figlio **Recordset**) viene inserito nella colonna del capitolo della riga corrente dell'elemento padre **Recordset**.  
  
6.  Quando si accede alla colonna del capitolo di un'altra riga, vengono ripetuti i passaggi 3-5.  
  
 Il **righe figlio della Cache** dinamica è impostata su **True** per impostazione predefinita. Il comportamento di memorizzazione nella cache varia in base ai valori di parametro della query. In una query con un singolo parametro, l'elemento figlio **Recordset** per un determinato parametro valore verrà memorizzato tra le richieste per un elemento figlio con tale valore. Il codice seguente illustra questo processo:  
  
```  
SCmd = "SHAPE {select * from customer} " & _  
         "APPEND({select * from orders where cust_id = ?} " & _  
         "RELATE cust_id TO PARAMETER 0) AS chpCustOrder"  
Rst1.Open sCmd, Cnn1  
Set RstChild = Rst1("chpCustOrder").Value  
Rst1.MoveNext      ' Next cust_id passed to Param 0, & new rs fetched   
                   ' into RstChild.  
Rst1.MovePrevious  ' RstChild now holds cached rs, saving round trip.  
```  
  
 In una query con due o più parametri, un elemento figlio memorizzati nella cache viene usato solo se i valori dei parametri corrispondono ai valori memorizzati nella cache.  
  
## <a name="parameterized-commands-and-complex-parent-child-relations"></a>I comandi con parametri e relazioni complesse padre-figlio  
 Oltre a usare i comandi con parametri per migliorare le prestazioni di una gerarchia di tipo equijoin, è possono utilizzare i comandi con parametri per supportare più complesse relazioni padre-figlio. Ad esempio, si consideri un database lega con due tabelle: un sistema costituito i team (team_id, team_name) e l'altro dei giochi (date, home_team, visiting_team).  
  
 Utilizzo di una gerarchia senza parametri, non è possibile correlare le tabelle di giochi e i team in modo che l'elemento figlio **Recordset** per ogni team contiene la pianificazione completa. È possibile creare capitoli che contengono la pianificazione iniziale o la pianificazione di viaggio, ma non entrambi. Infatti, la clausola RELATE è limitato a relazioni padre-figlio del form (pc1 = cc1) AND (pc2 = pc2). Pertanto, se il comando include "Sono correlati team_id a home_team, team_id TO visiting_team", si otterrebbe solo giochi in cui un team ricopriva stesso. È invece preferibile "(team_id=home_team) o (team_id = visiting_team)", ma il provider Shape non supporta la clausola OR.  
  
 Per ottenere il risultato desiderato, è possibile usare un comando con parametri. Ad esempio:  
  
```  
SHAPE {SELECT * FROM teams}   
APPEND ({SELECT * FROM games WHERE home_team = ? OR visiting_team = ?}   
        RELATE team_id TO PARAMETER 0,   
               team_id TO PARAMETER 1)   
```  
  
 In questo esempio sfrutta la maggiore flessibilità nella clausola WHERE SQL per ottenere il risultato che è necessario.  
  
> [!NOTE]
>  Quando nelle clausole WHERE, parametri possano non usare i tipi di dati SQL per text, ntext e image o verrà generato un errore che contiene la descrizione seguente: `Invalid operator for data type`.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di Data Shaping](../../../ado/guide/data/data-shaping-example.md)   
 [Grammatica formale per Shape](../../../ado/guide/data/formal-shape-grammar.md)   
 [Comandi Shape in generale](../../../ado/guide/data/shape-commands-in-general.md)
