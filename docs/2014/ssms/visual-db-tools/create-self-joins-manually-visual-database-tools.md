---
title: Creare self-join in modo manuale (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- self-joins
- manual joins [SQL Server]
- joins [SQL Server], self
ms.assetid: 910ed516-cb84-481b-95d0-cba3e89afdba
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dd8e26099ec7152aac08a11b6f7e38550834d248
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63184250"
---
# <a name="create-self-joins-manually-visual-database-tools"></a>Creazione di self-join in modo manuale (Visual Database Tools)
  È possibile unire in join una tabella con se stessa anche se questa non ha una relazione riflessiva nel database. È ad esempio possibile utilizzare un self-join per individuare coppie di autori che risiedono nella stessa città.  
  
 Come per tutti i tipi di join, un self-join richiede almeno due tabelle, con la differenza che, anziché aggiungere una seconda tabella alla query, si aggiungerà una seconda istanza della stessa tabella. Sarà così possibile confrontare una colonna nella prima istanza della tabella con la stessa colonna nella seconda istanza, in modo da confrontare fra loro i valori contenuti in una colonna. In [Progettazione query e Progettazione viste](visual-database-tools.md) verrà assegnato un alias alla seconda istanza della tabella.  
  
 Se ad esempio si crea un self-join per trovare tutte le coppie di autori di Berkeley, verrà confrontata la colonna `city` nella prima istanza della tabella con la colonna `city` nella seconda istanza. La query risultante potrebbe essere analoga alla seguente:  
  
```  
SELECT   
      authors.au_fname,   
      authors.au_lname,   
      authors1.au_fname AS Expr2,   
      authors1.au_lname AS Expr3  
   FROM   
      authors   
         INNER JOIN  
         authors authors1   
            ON authors.city   
             = authors1.city  
   WHERE  
      authors.city = 'Berkeley'  
```  
  
 La creazione di un self-join spesso richiede più condizioni di join. Il risultato della query precedente può essere utile per comprenderne la motivazione:  
  
```  
Cheryl Carson       Cheryl Carson  
Abraham Bennet      Abraham Bennet  
Cheryl Carson       Abraham Bennet  
Abraham Bennet      Cheryl Carson  
```  
  
 La prima riga è inutile: indica che Cheryl Carson vive nella stessa città di Cheryl Carson. Altrettanto inutile è la seconda riga. Per eliminare questi dati inutili, è possibile aggiungere un'altra condizione che consenta di conservare solo i risultati in cui i due nomi identificano autori diversi. La query risultante sarà analoga alla seguente:  
  
```  
SELECT   
      authors.au_fname,   
      authors.au_lname,   
      authors1.au_fname AS Expr2,   
      authors1.au_lname AS Expr3  
   FROM   
      authors   
         INNER JOIN  
         authors authors1   
            ON authors.city   
             = authors1.city  
            AND authors.au_id  
             <> authors1.au_id  
   WHERE  
      authors.city = 'Berkeley'  
```  
  
 Il set di risultati è migliorato:  
  
```  
Cheryl Carson       Abraham Bennet  
Abraham Bennet      Cheryl Carson  
```  
  
 Le due righe di risultati, tuttavia, sono ridondanti. La prima dice che Carson vive nella stessa città di Bennet e la seconda dice che Bennet vive nella stessa città di Carson. Per eliminare questa ridondanza, è possibile modificare la seconda condizione di join da "non uguale" a "minore di". La query risultante sarà analoga alla seguente:  
  
```  
SELECT   
      authors.au_fname,   
      authors.au_lname,   
      authors1.au_fname AS Expr2,   
      authors1.au_lname AS Expr3  
   FROM   
      authors   
         INNER JOIN  
         authors authors1   
            ON authors.city   
             = authors1.city  
            AND authors.au_id  
             < authors1.au_id  
   WHERE  
      authors.city = 'Berkeley'  
```  
  
 Si otterrà così un set di risultati analogo al seguente:  
  
```  
Cheryl Carson       Abraham Bennet  
```  
  
### <a name="to-create-a-self-join-manually"></a>Per creare manualmente un self-join  
  
1.  Aggiungere la tabella o l'oggetto con valori di tabella al riquadro [Diagramma](diagram-pane-visual-database-tools.md) .  
  
2.  Aggiungere nuovamente la stessa tabella o lo stesso oggetto con valori di tabella in modo che venga visualizzato due volte nel riquadro Diagramma.  
  
     Un alias verrà assegnato alla seconda istanza aggiungendo un numero sequenziale al nome della tabella. Verrà inoltre inserita una linea di join tra le due occorrenze della tabella o dell'oggetto con valori di tabella all'interno del riquadro Diagramma.  
  
3.  Fare clic con il pulsante destro del mouse sulla linea di join e scegliere **Proprietà** dal menu di scelta rapida.  
  
4.  Nella finestra Proprietà fare clic su **Condizione e tipo di join** e sui **puntini di sospensione (...)** a destra della proprietà.  
  
5.  Nella [finestra di dialogo Join](join-dialog-box-visual-database-tools.md) cambiare l'operatore di confronto tra le chiavi primarie secondo necessità. È ad esempio possibile modificare l'operatore minore di (<).  
  
6.  Creare l'altra condizione di join, ad esempio authors.zip = authors1.zip, trascinando il nome della colonna join primaria nella prima occorrenza della tabella o dell'oggetto con valori di tabella e rilasciandolo sulla colonna corrispondente nella seconda occorrenza.  
  
7.  Specificare le altre opzioni per la query, quali le colonne di output, le condizioni di ricerca e il criterio di ordinamento.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di self-join automaticamente &#40;Visual Database Tools&#41;](create-self-joins-automatically-visual-database-tools.md)   
 [Eseguire query con join &#40;Visual Database Tools&#41;](query-with-joins-visual-database-tools.md)  
  
  
