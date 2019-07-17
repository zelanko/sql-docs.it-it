---
title: Collegare le applicazioni di accesso al database SQL di Azure - SQL Server | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases, linking to SQL Azure
- Access databases, linking to SQL Server
- auto-increment columns
- data types, unsupported
- hyperlink columns
- linking tables
- migrating databases, post-migration issues
- post-migration issues
- reference, post-migration issues
- refreshing linked tables
- slow performance
- unlinking tables
ms.assetid: 82374ad2-7737-4164-a489-13261ba393d4
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 115aa0db8e8d6f2fdc35718ccb60f1d0ed06b5c1
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68259906"
---
# <a name="linking-access-applications-to-sql-server---azure-sql-db-accesstosql"></a>Collegamento delle applicazioni di accesso a SQL Server - database SQL di Azure (AccessToSQL)
Se si desidera utilizzare le applicazioni Access esistenti con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile collegare le tabelle di Access originale dopo la migrazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tabelle di SQL Azure. Collegamento è possibile modificare il database di Access in modo che le pagine di accesso di query, form, i report e dati usano i dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database di SQL Azure anziché i dati presenti nel database di Access.  
  
> [!NOTE]  
> L'accesso alle tabelle rimangono in Access, ma non vengono aggiornate insieme a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o gli aggiornamenti di SQL Azure. Dopo che si collegano le tabelle e verificare le funzionalità, è possibile eliminare le tabelle di Access.  
  
## <a name="linking-access-and-sql-server-tables"></a>Collegamento delle tabelle di Access e SQL Server  
Quando si collega una tabella di accesso a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tabella di SQL Azure, il motore di database Jet archivia le informazioni di connessione e i metadati della tabella, ma i dati vengono archiviati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Questo collegamento consente le applicazioni Access funzionano a fronte delle tabelle del database anche se le tabelle effettive e i dati sono [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
> [!NOTE]  
> Se si usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione, la password verrà archiviato come testo non crittografato in tabelle del database collegate. È consigliabile usare l'autenticazione di Windows.  
  
**Per collegare le tabelle**  
  
1.  Nel Visualizzatore metadati di accesso, selezionare le tabelle che si desidera collegare.  
  
2.  Fare doppio clic su **tabelle**, quindi selezionare **collegamento**.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) per l'accesso esegue il backup della tabella di Access originale e crea una tabella collegata.  
  
Dopo aver collegato le tabelle, le tabelle in SSMA vengono visualizzati con un'icona di collegamento di piccole dimensioni. In Access e le tabelle vengono visualizzati con un'icona "collegata", ovvero un mondo con una freccia che punta a esso.  
  
Quando si apre una tabella di Access, i dati vengono recuperati utilizzando un cursore keyset. Di conseguenza, per le tabelle di grandi dimensioni, tutti i dati non vengono recuperati in una sola volta. Tuttavia, durante l'esplorazione tramite la tabella, l'accesso consente di recuperare dati aggiuntivi in base alle esigenze.  
  
> [!IMPORTANT]  
> Per collegare l'accesso alle tabelle con un database di Azure, è necessario SQL Server Native Client(SNAC) versione 10.5 o versione successiva.   
> È possibile ottenere la versione più recente di SNAC dal [Microsoft® SQL Server® 2008 R2 Feature Pack](https://go.microsoft.com/fwlink/?LinkId=196940).  
  
## <a name="unlinking-access-tables"></a>Scollegamento accedere alle tabelle  
Quando si scollega una tabella di Access da un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tabella di SQL Azure, SSMA consente di ripristinare la tabella di Access originale e i relativi dati.  
  
**Scollegare le tabelle**  
  
1.  Nel Visualizzatore metadati di accesso, selezionare le tabelle che si desidera scollegare.  
  
2.  Fare doppio clic su **tabelle**, quindi selezionare **Unlink**.  
  
## <a name="linking-tables-to-a-different-server"></a>Collegamento delle tabelle in un altro server  
Se l'accesso alle tabelle è stato collegato a un'istanza di SQL Server e si desidera modificare i collegamenti a un'altra istanza in un secondo momento, è necessario ricollegare le tabelle.  
  
**Per collegare le tabelle in un altro server**  
  
1.  Nel Visualizzatore metadati di accesso, selezionare le tabelle che si desidera scollegare.  
  
2.  Fare doppio clic su **tabelle** e quindi selezionare **Unlink**.  
  
3.  Scegliere il **Riconnetti a SQL Server** pulsante.  
  
4.  Connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure a cui si desidera collegare l'accesso alle tabelle.  
  
5.  Nel Visualizzatore metadati di accesso, selezionare le tabelle che si desidera collegare.  
  
6.  Fare doppio clic su **tabelle**, quindi selezionare **collegamento**.  
  
## <a name="updating-linked-tables"></a>Aggiornamento delle tabelle collegate  
Se il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o vengono modificati le definizioni delle tabelle di SQL Azure, è possibile scollegare e quindi collegare nuovamente le tabelle in SSMA usando le procedure illustrate in precedenza in questo argomento. È anche possibile aggiornare le tabelle utilizzando l'accesso.  
  
**Per aggiornare le tabelle collegate utilizzando l'accesso**  
  
1.  Aprire il database di Access.  
  
2.  Nel **oggetti** fare clic su **tabelle**.  
  
3.  Fare doppio clic su una tabella collegata e quindi selezionare **gestore tabelle collegate**.  
  
4.  Selezionare la casella di controllo accanto a ogni tabella collegata che si desidera aggiornare e quindi fare clic su **OK**.  
  
## <a name="possible-post-migration-issues"></a>Possibili problemi di post-migrazione  
Le sezioni seguenti problemi di elenco che potrebbero verificarsi nelle applicazioni Access esistenti dopo la migrazione di database da Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure e quindi collegare le tabelle, insieme alle cause e le risoluzioni.  
  
### <a name="slow-performance-with-linked-tables"></a>Rallentamento delle prestazioni con le tabelle collegate  
**Causa:** Alcune query potrebbero essere lente dopo upsizing per i motivi seguenti:  
  
-   L'applicazione dipende dalle funzioni che non esistono nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, provocando Jet per le tabelle in locale per eseguire una query di selezione a discesa.  
  
-   Le query che aggiornano o eliminano molte righe vengono inviate da Jet come una query con parametri per ogni riga.  
  
**Soluzione:** Convertire le query a esecuzione lenta query pass-through, viste o stored procedure. La conversione in query pass-through presenta i seguenti problemi:  
  
-   Le query pass-through non possono essere modificate. Modifica il risultato della query o l'aggiunta di nuovi record deve essere eseguita in un modo alternativo, ad esempio dal visto esplicita **Modify** oppure **Add** pulsanti nel form che è associato alla query.  
  
-   Alcune query richiedono l'input dell'utente, ma non supportano le query pass-through input dell'utente. Input dell'utente può essere ottenuto da codice Applications (VBA) che vengono richiesti i parametri di Visual Basic o da un modulo che viene usato come un controllo di input. In entrambi i casi, il codice VBA invia la query con l'input dell'utente al server.  
  
### <a name="auto-increment-columns-are-not-updated-until-the-record-is-updated"></a>Colonne a incremento automatico non vengono aggiornate finché il record viene aggiornato  
**Causa:** Dopo aver chiamato RecordSet.AddNew Jet, la colonna a incremento automatico è disponibile prima che il record viene aggiornato. Non è impostata su true nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Il nuovo valore del valore nuovo della colonna identity è disponibile solo dopo aver salvato il nuovo record.  
  
**Soluzione:** Eseguire il codice Visual Basic Applications Edition (VBA) prima l'accesso al campo di identità:  
  
```  
Recordset.Update  
Recordset.Move 0,  
Recordset.LastModified  
```  
  
### <a name="new-records-are-not-available"></a>Non sono disponibili nuovi record  
**Causa:** Quando si aggiunge un record a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o una tabella di SQL Azure utilizzando VBA, se il campo di indice univoci della tabella ha un valore predefinito e si assegna un valore a tale campo, non viene visualizzato il nuovo record fino a quando non si riapre la tabella in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Se si prova a ottenere un valore dal nuovo record, è visualizzato il messaggio di errore seguente:  
  
`Run-time error '3167' Record is deleted.`  
  
**Soluzione:** Quando si apre la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure tramite il codice VBA di tabella, includere il `dbSeeChanges` opzione, come nell'esempio seguente:  
  
`Set rs = db.OpenRecordset("TestTable", dbOpenDynaset, dbSeeChanges)`  
  
### <a name="after-migration-some-queries-will-not-allow-the-user-to-add-a-new-record"></a>Dopo la migrazione, alcune query non consentirà all'utente di aggiungere un nuovo record  
**Causa:** Se una query non include tutte le colonne che sono inclusi in un indice univoco, è possibile aggiungere nuovi valori utilizzando la query.  
  
**Soluzione:** Verificare che tutte le colonne incluse in almeno un indice univoco facciano parte della query.  
  
### <a name="you-cannot-modify-a-linked-table-schema-with-access"></a>Non è possibile modificare uno schema di tabella collegata con accesso  
**Causa:** Dopo la migrazione dei dati e le tabelle di collegamento, l'utente non è possibile modificare lo schema di una tabella di Access.  
  
**Soluzione:** Modificare lo schema della tabella usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e quindi aggiornare il collegamento di accesso.  
  
### <a name="hyperlink-functionality-is-lost-after-migrating-data"></a>La funzionalità di collegamento ipertestuale viene persa dopo la migrazione dei dati  
**Causa:** Dopo la migrazione di dati, collegamenti ipertestuali nelle colonne le loro funzionalità vadano perse e diventano semplici **nvarchar (max)** colonne.  
  
**Soluzione:** No.  
  
### <a name="some-sql-server-data-types-are-not-supported-by-access"></a>Alcuni tipi di dati di SQL Server non sono supportati da Access  
**Causa:** Se si aggiorna in un secondo momento le [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tabelle di SQL Azure contengono i tipi di dati che non sono supportati da accesso, non è possibile aprire la tabella di Access.  
  
**Soluzione:** È possibile definire una query di accesso che restituisce solo le righe con tipi di dati supportati.  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database di Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
