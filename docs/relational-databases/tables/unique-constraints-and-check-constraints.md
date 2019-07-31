---
title: Vincoli UNIQUE e CHECK | Microsoft Docs
ms.custom: ''
ms.date: 06/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- constraints [SQL Server], Visual Database Tools
- Visual Database Tools [SQL Server], constraints
ms.assetid: 637098af-2567-48f8-90f4-b41df059833e
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 400b028696666b188760f61c2490a218bc8bd2be
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017666"
---
# <a name="unique-constraints-and-check-constraints"></a>Vincoli UNIQUE e CHECK
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  I vincoli UNIQUE e CHECK sono due tipi di vincoli che possono essere utilizzati per applicare l'integrità dei dati nelle tabelle di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si tratta di importanti oggetti di database.  
  
 In questo argomento sono contenute le sezioni seguenti.  
  
 [Vincoli UNIQUE](#Unique)  
  
 [Vincoli CHECK](#Check)  
  
 [Attività correlate](#Tasks)  
  
##  <a name="Unique"></a> Vincoli UNIQUE  
 I vincoli sono regole attivate dal [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . È possibile ad esempio utilizzare i vincoli UNIQUE per garantire che non vengano immessi valori duplicati in colonne specifiche che non fanno parte di una chiave primaria. Sebbene sia i vincoli UNIQUE che i vincoli PRIMARY KEY applichino l'univocità, utilizzare un vincolo UNIQUE anziché un vincolo PRIMARY KEY se si desidera applicare l'univocità di una colonna, o di una combinazione di colonne, che non costituisce la chiave primaria.  
  
 A differenza dei vincoli PRIMARY KEY, i vincoli UNIQUE supportano il valore NULL. Tuttavia, come per qualsiasi valore che fa parte di un vincolo UNIQUE, è consentito un solo valore Null per colonna. A un vincolo UNIQUE può fare riferimento un vincolo FOREIGN KEY.  
  
 Quando un vincolo UNIQUE viene aggiunto a una o più colonne esistenti nella tabella, per impostazione predefinita i dati esistenti nelle colonne vengono esaminati dal [!INCLUDE[ssDE](../../includes/ssde-md.md)] per verificare che tutti i valori siano univoci. Se un vincolo UNIQUE viene aggiunto a una colonna che contiene valori duplicati, [!INCLUDE[ssDE](../../includes/ssde-md.md)] restituisce un errore e il vincolo non viene aggiunto.  
  
 In [!INCLUDE[ssDE](../../includes/ssde-md.md)] viene creato automaticamente un indice UNIQUE per imporre il requisito di univocità del vincolo UNIQUE. Se, pertanto, si tenta di inserire una riga duplicata, in [!INCLUDE[ssDE](../../includes/ssde-md.md)] viene restituito un messaggio di errore che indica che il vincolo UNIQUE è stato violato e che la riga non verrà aggiunta alla tabella. Se non si specifica in modo esplicito un indice cluster, per impostazione predefinita viene creato un indice univoco non cluster per applicare il vincolo UNIQUE.  
  
##  <a name="Check"></a> Vincoli CHECK  
 I vincoli CHECK assicurano l'integrità di dominio limitando i valori accettati da una o più colonne. È possibile creare un vincolo CHECK con qualsiasi espressione logica (booleana) che restituisce TRUE o FALSE in base agli operatori logici. È ad esempio possibile limitare l'intervallo di valori di una colonna **salary** creando un vincolo CHECK che consente solo dati compresi tra 15.000 e 100.000 euro. In questo modo si evita di inserire stipendi con valori non compresi nell'intervallo regolare. L'espressione logica potrebbe essere la seguente: `salary >= 15000 AND salary <= 100000`.  
  
 È possibile applicare più vincoli CHECK a una colonna e inoltre applicare un singolo vincolo CHECK a più colonne creandolo a livello di tabella. È ad esempio possibile usare un vincolo CHECK in più colonne per confermare che a ogni riga con un valore di colonna **country_region** pari a **USA** corrisponda un valore di due caratteri nella colonna **state** . In questo modo è possibile verificare più condizioni simultaneamente.  
  
 I vincoli CHECK simili ai vincoli FOREIGN KEY perché controllano i valori inseriti in una colonna. La differenza consiste nel modo in cui determinano i valori validi. I vincoli FOREIGN KEY ottengono l'elenco di valori validi da un'altra tabella, mentre i vincoli CHECK determinano i valori validi da un'espressione logica.  
  
> [!CAUTION]  
>  I vincoli che prevedono la conversione implicita o esplicita di tipi di dati possono impedire l'esecuzione di operazioni specifiche. Ad esempio, i vincoli definiti nelle tabelle di origine per il cambio di partizione possono impedire l'esecuzione di un'operazione ALTER TABLE...SWITCH. Evitare la conversione di tipi di dati nelle definizioni dei vincoli.  
  
### <a name="limitations-of-check-constraints"></a>Limitazioni per i vincoli CHECK  
 I vincoli CHECK non accettano i valori che restituiscono FALSE. I valori Null restituiscono UNKNOWN e pertanto se vengono inseriti in un'espressione è possibile che un vincolo venga ignorato. Si supponga, ad esempio, di inserire un vincolo su una colonna di tipo **int** denominata **MyColumn** e di specificare che **MyColumn** possa contenere solo il valore 10:**MyColumn=10**. Se si inserisce il valore NULL in **MyColumn**, [!INCLUDE[ssDE](../../includes/ssde-md.md)] inserisce NULL e non restituisce un errore.  
  
 Un vincolo CHECK restituisce TRUE se la verifica della condizione controllata non restituisce FALSE per nessuna riga della tabella. Un vincolo CHECK viene utilizzato a livello di riga. Se una tabella appena creata non contiene righe, tutti i vincoli CHECK sulla tabella sono considerati validi. Questa situazione può generare risultati imprevisti, come è illustrato nell'esempio seguente.  
  
```  
CREATE TABLE CheckTbl (col1 int, col2 int);  
GO  
CREATE FUNCTION CheckFnctn()  
RETURNS int  
AS   
BEGIN  
   DECLARE @retval int  
   SELECT @retval = COUNT(*) FROM CheckTbl  
   RETURN @retval  
END;  
GO  
ALTER TABLE CheckTbl  
ADD CONSTRAINT chkRowCount CHECK (dbo.CheckFnctn() >= 1 );  
GO  
```  
  
 Il vincolo `CHECK` inserito specifica che deve essere presente almeno una riga nella tabella `CheckTbl`. Poiché nella tabella non sono presenti righe per le quali è possibile verificare la condizione del vincolo, l'istruzione ALTER TABLE ha tuttavia esito positivo.  
  
 I vincoli CHECK non vengono convalidati durante l'esecuzione di istruzioni DELETE. L'esecuzione di istruzioni DELETE su tabelle che includono tipi di vincoli CHECK specifici può pertanto generare risultati imprevisti. Ad esempio, si considerino le istruzioni seguenti eseguite sulla tabella `CheckTbl`.  
  
```  
INSERT INTO CheckTbl VALUES (10, 10);  
GO  
DELETE CheckTbl WHERE col1 = 10;  
```  
  
 L'istruzione `DELETE` ha esito positivo, anche se il vincolo `CHECK` specifica che la tabella `CheckTbl` deve contenere almeno `1` riga.  
  
##  <a name="Tasks"></a> Attività correlate  
  
> [!NOTE]  
>  Se la tabella viene pubblicata per la replica, è necessario apportare modifiche allo schema usando l'istruzione [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) di Transact-SQL oppure SMO (SQL Server Management Objects). Quando si apportano modifiche allo schema utilizzando Progettazione tabelle o Progettazione diagrammi di database, viene effettuato il tentativo di rimuovere e rigenerare la tabella. La modifica allo schema non riuscirà, poiché non è consentita la rimozione di oggetti pubblicati.  
  
|Attività|Argomento|  
|----------|-----------|  
|Viene descritto come creare un vincolo UNIQUE.|[Creare vincoli univoci](../../relational-databases/tables/create-unique-constraints.md)|  
|Viene descritto come modificare un vincolo UNIQUE.|[Modificare vincoli univoci](../../relational-databases/tables/modify-unique-constraints.md)|  
|Viene descritto come eliminare un vincolo UNIQUE.|[Eliminazione di vincoli univoci](../../relational-databases/tables/delete-unique-constraints.md)|  
|Viene descritto come disabilitare un vincolo CHECK quando un agente di replica inserisce o aggiorna i dati nella tabella.|[Disabilitare un vincolo CHECK per la replica](../../relational-databases/tables/disable-check-constraints-for-replication.md)|  
|Viene descritto come disabilitare un vincolo CHECK quando vengono aggiunti, aggiornati o eliminati dati in una tabella.|[Disabilitazione di vincoli CHECK con le istruzioni INSERT e UPDATE](../../relational-databases/tables/disable-check-constraints-with-insert-and-update-statements.md)|  
|Viene descritto come modificare l'espressione del vincolo o le opzioni che abilitano o disabilitano il vincolo se si verificano determinate condizioni.|[Modifica di vincoli CHECK](../../relational-databases/tables/modify-check-constraints.md)|  
|Viene descritto come eliminare un vincolo CHECK.|[Eliminazione dei vincoli CHECK](../../relational-databases/tables/delete-check-constraints.md)|  
|Viene descritto come visualizzare le proprietà di un vincolo CHECK.|[Vincoli UNIQUE e CHECK](../../relational-databases/tables/unique-constraints-and-check-constraints.md)|  
  
  
