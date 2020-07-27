---
title: Impostazione copia tabella o query (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.specifytablecopyorquery.f1
ms.assetid: 08aa7158-40e6-4ef3-84d3-1265a8ba194c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: da112bf3a58d33fd7fae154d5a437c309ab7d2a6
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86914344"
---
# <a name="specify-table-copy-or-query-sql-server-import-and-export-wizard"></a>Impostazione copia tabella o query (Importazione/Esportazione guidata SQL Server)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Dopo aver fornito informazioni sulla destinazione dei dati e su come connettersi a tale destinazione, l'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostra la pagina **Impostazione copia tabella o query**. In questa pagina è possibile scegliere una delle opzioni seguenti.
-   **Copia i dati da una o più tabelle o viste**. Per selezionare una o più tabelle da un elenco.
-   **Scrivi una query per specificare i dati da trasferire**. Per immettere o incollare il testo di una query SQL.
    
> [!TIP]
> Se è necessario copiare più di un database oppure oggetti di database diversi da tabelle e viste, usare Copia guidata database anziché l'Importazione/Esportazione guidata. Per altre informazioni, vedere [Utilizzo di Copia guidata database](../../relational-databases/databases/use-the-copy-database-wizard.md).     
 
## <a name="screen-shot-of-the-specify-table-copy-or-query-page"></a>Screenshot della pagina Impostazione copia tabella o query    
 La schermata seguente mostra la pagina **Impostazione copia tabella o query** della procedura guidata.    
    
 ![Pagina Impostazione copia tabella o query dell'Importazione/Esportazione guidata](../../integration-services/import-export-data/media/table-copy-or-query.png "Pagina Impostazione copia tabella o query dell'Importazione/Esportazione guidata")    
    
## <a name="specify-whether-to-copy-an-entire-table-or-write-a-query"></a>Specificare se copiare un'intera tabella o scrivere una query 
 **Copia i dati da una o più tabelle o viste**    
 Selezionare questa opzione se si vogliono copiare i dati dell'origine senza filtrare o ordinare i record.   

Se si seleziona **Copia i dati da una o più tabelle o viste**, è possibile eseguire la copia da una tabella o vista nella tabella di destinazione o da più tabelle o viste in più tabelle di destinazione.

 Dopo aver fatto clic **Avanti**, selezionare le tabelle da copiare nella pagina **Seleziona tabelle e viste di origine** . Per altre informazioni, vedere [Selezione tabelle e viste di origine](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md).   
    
 **Scrivi una query per specificare i dati da trasferire**    
 Selezionare questa opzione se si vuole filtrare o ordinare i dati di origine prima di copiarli nella destinazione.    
    
Se si seleziona **Scrivi una query per specificare i dati da trasferire**, è possibile copiare nella tabella di destinazione solo i risultati di una query .  

Dopo aver fatto clic **Avanti**, specificare un'istruzione SQL per impostare le colonne e selezionare le righe nella finestra di dialogo **Impostazione query di origine** . Per altre informazioni, vedere [Impostazione query di origine](../../integration-services/import-export-data/provide-a-source-query-sql-server-import-and-export-wizard.md).   
    
## <a name="why-isnt-the-copy-option-available"></a>Perché l'opzione di copia non è disponibile?    
 L'opzione **Copia i dati da una o più tabelle o viste** potrebbe non essere disponibile quando la procedura guidata usa un provider di dati [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] per la connessione all'origine dati. In questo caso, infatti, la procedura guidata non dispone di informazioni sufficienti sul provider di dati per richiedere un elenco di tabelle e viste dall'origine dati. 
 
È possibile usare l'opzione **Scrivi una query** anche se in genere non si scrivono query SQL, purché si conosca il nome della tabella da esportare. Nella finestra di dialogo **Impostazione query di origine**, visualizzata quando si fa clic su **Avanti**, immettere la query come `SELECT * FROM <name of table>`. Se il nome della tabella contiene spazi o altri caratteri speciali, racchiudere il nome tra parentesi quadre - `SELECT * FROM [<name of table>]`.

### <a name="more-info"></a>Altre informazioni
 L'opzione **Copia i dati da una o più tabelle o viste** è disponibile solo per i provider per i quali è presente una sezione ProviderDescription nel file ProviderDescriptors.xml. Per impostazione predefinita, questo file si trova in \<*drive*>:\Programmi\Microsoft SQL Server\130\DTS\ProviderDescriptors. Ogni sezione ProviderDescription del file contiene le informazioni necessarie per recuperare metadati dal provider corrispondente.    
    
 Per impostazione predefinita, il file ProviderDescriptors.xml contiene una sezione ProviderDescription solo per i provider seguenti:    
    
-   Provider di dati .Net Framework per SQL Server (System.Data.SqlClient)    
    
-   Provider di dati .Net Framework per Oracle (System.Data.OracleClient)    
    
-   Provider di dati .Net Framework per ODBC (System.Data.Odbc)    
    
-    System.Data.OleDb (applicabile a tutti i provider OLE DB)    
    
-   Provider Microsoft per DB2 installato da Microsoft Host Integration Server (Microsoft.HostIntegration.MsDb2Client.MsDb2Connection)    
    
 Sviluppatori di terze parti possono rendere disponibile l'opzione **Copia i dati da una o più tabelle o viste** ad altri provider aggiungendo una sezione ProviderDescriptor al file ProviderDescriptors.xml. Per verificare i requisiti per la sezione ProviderDescriptor, vedere il file di schema ProviderDescriptors.xsd disponibile, per impostazione predefinita, nella stessa cartella del file ProviderDescriptors.xml.    
    
## <a name="whats-next"></a>Quali sono le operazioni successive?    
 Dopo aver specificato se si vuole copiare un'intera tabella o eseguire una query, la pagina successiva dipende dall'opzione selezionata in questa pagina e dalla destinazione dei dati.    
    
-   Se è stata selezionata l'opzione **Copia i dati da una o più tabelle o viste**, la pagina successiva è **Seleziona tabelle e viste di origine**per la maggior parte delle destinazioni. In questa pagina è possibile selezionare le tabelle e le viste esistenti da copiare nella destinazione dall'origine dati. Per altre informazioni, vedere [Selezione tabelle e viste di origine](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md).    
    
-   Se è stata selezionata l'opzione **Copia i dati da una o più tabelle o viste** e la destinazione è un file flat, la pagina successiva è **Configurare la destinazione del file flat**. In questa pagina è possibile specificare le opzioni di formattazione per il file flat di destinazione. (quindi, dopo aver configurato il file flat, la pagina successiva sarà **Seleziona tabelle e viste di origine**). Per altre informazioni, vedere [Configurazione destinazione file flat](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md).    
    
-   Se è stata selezionata l'opzione **Scrivi una query per specificare i dati da trasferire**, la pagina successiva è **Impostazione query di origine**. In questa pagina è necessario scrivere e testare l'istruzione SQL che seleziona i dati da copiare nella destinazione dall'origine dati (quindi, dopo aver impostato la query, la pagina successiva sarà **Seleziona tabelle e viste di origine**). Per altre informazioni, vedere [Impostazione query di origine](../../integration-services/import-export-data/provide-a-source-query-sql-server-import-and-export-wizard.md).

## <a name="see-also"></a>Vedere anche
[Iniziare con questo semplice esempio dell'Importazione/Esportazione guidata](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)


