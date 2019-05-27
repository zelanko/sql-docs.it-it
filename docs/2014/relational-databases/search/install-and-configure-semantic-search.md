---
title: Installare e configurare la ricerca semantica | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], installing
- semantic search [SQL Server], configuring
ms.assetid: 2cdd0568-7799-474b-82fb-65d79df3057c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c7ac7238d643165bc093a8a1cabd5d1dac662dfc
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/22/2019
ms.locfileid: "66011136"
---
# <a name="install-and-configure-semantic-search"></a>Installazione e configurazione della ricerca semantica
  Vengono descritti i prerequisiti per la ricerca semantica statistica e viene indicato come installarli o verificarli.  
  
## <a name="installing-semantic-search"></a>Installazione della ricerca semantica  
  
###  <a name="HowToCheckInstalled"></a> Come si fa: Controllare se è installata la ricerca semantica  
 Eseguire una query sulla proprietà **IsFullTextInstalled** della funzione per i metadati [SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql).  
  
 Se viene restituito il valore 1, la ricerca full-text e la ricerca semantica sono installate. Se viene restituito il valore 0, le ricerche non sono installate.  
  
```sql  
SELECT SERVERPROPERTY('IsFullTextInstalled');  
GO  
```  
  
###  <a name="BasicsSemanticSearch"></a> Come si fa: Installare la ricerca semantica  
 Per installare la ricerca semantica, selezionare **Estrazioni full-text e semantiche per la ricerca** nella pagina **Funzionalità da installare** durante l'installazione.  
  
 La ricerca semantica statistica dipende dalla ricerca full-text. Queste due funzionalità facoltative di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vengono installate insieme.  
  
## <a name="installing-or-removing-the-semantic-language-statistics-database"></a>Installazione o rimozione del database di statistiche lingua semantica  
 La ricerca semantica dispone di una dipendenza esterna aggiuntiva denominata database di statistiche lingua semantica. Questo database contiene i modelli di lingua statistici richiesti dalla ricerca semantica. Un singolo database di statistiche lingua semantica contiene i modelli di lingua per tutte le lingue supportate per l'indicizzazione semantica.  
  
###  <a name="HowToCheckDatabase"></a> Come si fa: Controllare se il Database di statistiche lingua semantica è installato  
 Eseguire una query sulla vista del catalogo [sys.fulltext_semantic_language_statistics_database &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql).  
  
 Se il database di statistiche lingua semantica è installato e registrato per l'istanza, i risultati della query conterranno una sola riga di informazioni sul database.  
  
```vb  
SELECT * FROM sys.fulltext_semantic_language_statistics_database;  
GO  
```  
  
###  <a name="HowToInstallModel"></a> Come si fa: Installare, collegare e registrare il Database di statistiche lingua semantica  
 Il database di statistiche lingua semantica non viene installato dal programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Per configurare il database di statistiche lingua semantica come prerequisito per l'indicizzazione semantica, effettuare le operazioni seguenti:  
  
 **1. Installare il database di statistiche lingua semantica.**  
 1.  Individuare il database di statistiche lingua semantica sui supporti di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o scaricarlo dal Web.  
  
    -   Individuare il pacchetto di Windows Installer denominato **SemanticLanguageDatabase.msi** sui supporti di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Individuare la versione a 32 bit o la versione a 64 bit del pacchetto di installazione a seconda del sistema di destinazione. Il nome della cartella che contiene il file ne identifica la versione a 32 bit o a 64 bit; il nome del file stesso è uguale per entrambe versioni.  
  
    -   Scaricare il pacchetto di programma di installazione dal [Microsoft? SQL Server?? 2014 semantic Language Statistics](https://go.microsoft.com/fwlink/?LinkID=296743) pagina il [!INCLUDE[msCoName](../../../includes/msconame-md.md)] area Download Microsoft.  
  
2.  Eseguire il pacchetto di Windows Installer **SemanticLanguageDatabase.msi** per estrarre il database e il file di log.  
  
     Se lo si desidera, è possibile modificare la directory di destinazione. Per impostazione predefinita, il programma di installazione estrae i file in una cartella denominata **Microsoft Semantic Language Database** nella cartella Programmi a 32 o a 64 bit. Il file MSI contiene un file di database compresso e un file di log.  
  
3.  Spostare il file di database estratto e il file di log in un percorso appropriato nel file system.  
  
     Se i file vengono lasciati nel percorso predefinito, non sarà possibile estrarre un'altra copia del database per un'altra istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Quando viene estratto il database di statistiche lingua semantica, al file di database e al file di log nel percorso predefinito del file system vengono assegnate autorizzazioni limitate. Si potrebbe pertanto non disporre dell'autorizzazione per collegare il database se lo si lascia nel percorso predefinito. Se viene generato un errore quando si tenta di collegare il database, spostare i file o verificare e correggere le autorizzazioni del file system nel modo appropriato.  
  
 **2. Collegare il database di statistiche lingua semantica.**  
 Collegare il database all'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o chiamando [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql) con la sintassi **FOR ATTACH**. Per altre informazioni, vedere [Collegamento e scollegamento di un database &#40;SQL Server&#41;](../databases/database-detach-and-attach-sql-server.md).  
  
 Per impostazione predefinita, il nome del database è **semanticsdb**. Facoltativamente è possibile fornire un nome diverso per il database al momento del collegamento. Tale nome dovrà essere fornito al momento di registrare il database nel passaggio successivo.  
  
```sql  
CREATE DATABASE semanticsdb  
            ON ( FILENAME = 'C:\Microsoft Semantic Language Database\semanticsdb.mdf' )  
            LOG ON ( FILENAME = 'C:\Microsoft Semantic Language Database\semanticsdb_log.ldf' )  
            FOR ATTACH;  
GO  
```  
  
 In questo esempio di codice si presuppone che il database sia stato spostato dal percorso predefinito in un nuovo percorso.  
  
 **3. Registrare il database di statistiche lingua semantica.**  
 Chiamare la stored procedure [sp_fulltext_semantic_register_language_statistics_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-semantic-register-language-statistics-db-transact-sql) e specificare il nome assegnato al database al momento del collegamento.  
  
```sql  
EXEC sp_fulltext_semantic_register_language_statistics_db @dbname = N'semanticsdb';  
GO  
```  
  
###  <a name="HowToUnregister"></a> Come si fa: Annullare la registrazione, scollegare e rimuovere il Database di statistiche lingua semantica  
 **Annullare la registrazione del database di statistiche lingua semantica.**  
 Chiamare la stored procedure [sp_fulltext_semantic_unregister_language_statistics_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-semantic-unregister-language-statistics-db-transact-sql). Poiché un'istanza può includere un solo database di statistiche lingua semantica, non è necessario fornire il nome del database.  
  
```sql  
EXEC sp_fulltext_semantic_unregister_language_statistics_db;  
GO  
```  
  
 **Scollegare il database di statistiche lingua semantica.**  
 Chiamare la stored procedure [sp_detach_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-detach-db-transact-sql) e indicare il nome del database.  
  
```sql  
USE master;  
GO  
  
EXEC sp_detach_db @dbname = N'semanticsdb';  
GO  
```  
  
 **Rimuovere il database di statistiche lingua semantica.**  
 Dopo avere annullato la registrazione del database e averlo scollegato, è possibile eliminare semplicemente il file di database. Non è disponibile alcun programma di disinstallazione e non è presente alcuna voce in **Programmi e funzionalità** nel Pannello di controllo.  
  
###  <a name="reqinstall"></a> Requisiti e restrizioni per l'installazione e la rimozione del Database di statistiche lingua semantica  
  
-   È possibile collegare e registrare un solo database di statistiche lingua semantica in un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
     Ogni istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in un solo computer richiede una copia fisica separata del database di statistiche lingua semantica. Allegare una copia a ciascuna istanza.  
  
-   Non è possibile scollegare un database di statistiche lingua semantica valido e registrato e sostituirlo con un database arbitrario che abbia lo stesso nome. In questo caso, i popolamenti dell'indice attivi o successivi non riusciranno.  
  
-   Il database di statistiche lingua semantica è di sola lettura. Non è possibile personalizzare questo database. Se si modifica il contenuto del database in qualsiasi modo, i risultati per le successive indicizzazioni semantiche saranno non deterministici. Per ripristinare lo stato originale di questi dati, è possibile eliminare il database modificato e scaricare e collegare una nuova copia non modificata del database.  
  
-   È possibile scollegare o eliminare il database di statistiche lingua semantica. Se ad alcune operazioni di indicizzazione attive sono applicati blocchi in lettura per il database, lo scollegamento o l'eliminazione non riuscirà o si verificherà un timeout. Questo aspetto è coerente con il comportamento esistente. In seguito alla rimozione del database, qualsiasi operazione di indicizzazione semantica non riuscirà.  
  
## <a name="installing-optional-support-for-newer-document-types"></a>Installazione del supporto facoltativo per i tipi di documento più nuovi  
  
###  <a name="office"></a> Come si fa: Installa i filtri più recenti per Microsoft Office e altri tipi di documenti di Microsoft  
 In questa versione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vengono installati i word breaker e gli stemmer [!INCLUDE[msCoName](../../../includes/msconame-md.md)] più recenti, ma non vengono installati i filtri più recenti per i documenti di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Office e altri tipi di documento [!INCLUDE[msCoName](../../../includes/msconame-md.md)] . Questi filtri sono necessari per l'indicizzazione di documenti creati con le versioni recenti di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Office e di altre applicazioni [!INCLUDE[msCoName](../../../includes/msconame-md.md)] . Per scaricare i filtri più recenti, vedere [Microsoft Office 2010 Filter Pack](https://go.microsoft.com/fwlink/?LinkId=218293).  
  
  
