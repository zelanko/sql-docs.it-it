---
title: Eseguire SQL Server importazione / esportazione guidata | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Import and Export Wizard
- starting SQL Server Import and Export Wizard
- Import and Export Wizard
- starting Import and Export Wizard
ms.assetid: 5fc4f6d1-1f6f-444e-9aeb-827f85e1c405
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4a01ae02feae938c952096216b89858c007aee4f
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53351392"
---
# <a name="run-the-sql-server-import-and-export-wizard"></a>Esecuzione dell'Importazione/Esportazione guidata SQL Server
  Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] costituisce il metodo più semplice per la copia di dati tra origini dati e per la costruzione di pacchetti di base. Per altre informazioni sulla procedura guidata, vedere [SQL Server importazione / esportazione guidata](import-and-export-data-with-the-sql-server-import-and-export-wizard.md).  
  
 Per un video che illustra come usare SQL Server importazione / esportazione guidata per creare un pacchetto che Esporta dati da un database di SQL Server in un foglio di calcolo di Microsoft Excel, vedere [esportazione di dati di SQL Server in Excel (Video di SQL Server)](https://go.microsoft.com/fwlink/?LinkId=131024).  
  
### <a name="to-start-the-sql-server-import-and-export-wizard"></a>Per avviare Importazione/Esportazione guidata SQL Server  
  
-   Nel **avviare** dal menu **tutti i programmi**, scegliere**Microsoft SQL Server** e quindi fare clic su **importare ed esportare dati**.  
  
     oppure  
  
     Nelle [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], fare doppio clic il **pacchetti SSIS** cartella e quindi fare clic su **SSISImport / esportazione guidata**.  
  
     oppure  
  
     Nella [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]via il **Project** menu, fare clic su **SSISImport / esportazione guidata**.  
  
     oppure  
  
     Nella [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)] tipo di server, espandere database, fare doppio clic su un database, scegliere **attività**e quindi fare clic su **Import Data** o **esportare i dati**.  
  
     oppure  
  
     In una finestra del prompt dei comandi eseguire DTSWizard.exe, disponibile in C:\Programmi\Microsoft SQL Server\100\DTS\Binn.  
  
    > [!NOTE]  
    >  In un computer a 64 bit con [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] viene installata la versione a 64 bit dell'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (DTSWizard.exe). Tuttavia, alcune origini dati, ad esempio Access o Excel, dispongono solo di un provider a 32 bit. Per utilizzare queste origini dati, potrebbe essere necessario installare ed eseguire la versione a 32 bit della procedura guidata. Per installare la versione a 32 bit della procedura guidata, selezionare gli strumenti client o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] durante l'installazione.  
  
### <a name="to-import-or-export-data-by-using-the-sql-server-import-and-export-wizard"></a>Per importare o esportare i dati utilizzando l'Importazione/Esportazione guidata SQL Server  
  
1.  Avviare l'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Nelle pagine della procedura guidata corrispondenti selezionare un'origine e una destinazione dei dati.  
  
     Le origini dati disponibili includono i provider di dati [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], i provider OLE DB, i provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, i provider [!INCLUDE[vstecado](../../includes/vstecado-md.md)], Microsoft Office Excel, Microsoft Office Access e l'origine file flat. A seconda dell'origine, è necessario impostare opzioni quali la modalità di autenticazione, il nome del server, il nome del database e il formato del file.  
  
    > [!NOTE]  
    >  Il provider [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB per Oracle non supporta i tipi di dati Oracle BLOB, CLOB, NCLOB, BFILE e UROWID. Pertanto, l'origine OLE DB non è in grado di estrarre i dati da tabelle che contengono colonne con tali tipi di dati.  
  
     Le destinazioni dei dati disponibili includono i provider di dati [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], i provider OLE DB, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, Excel, Access e la destinazione file flat.  
  
3.  Impostare le opzioni per il tipo di destinazione selezionato.  
  
     Se la destinazione è un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], sarà possibile:  
  
    -   Indicare se creare un nuovo database e impostarne le proprietà. Non è possibile configurare le proprietà seguenti, per le quali vengono utilizzati i valori predefiniti specificati:  
  
        |Proprietà|Value|  
        |--------------|-----------|  
        |Confronto|Latin1_General_CS_AS_KS_WS|  
        |modello di recupero|Full|  
        |Usa indicizzazione full-text|True|  
  
    -   Selezionare se copiare i dati da tabelle o viste oppure copiare risultati di query.  
  
         Se si desidera eseguire una query sull'origine dei dati e copiare i risultati, sarà possibile creare una query Transact-SQL. È possibile immettere la query Transact-SQL manualmente o utilizzare una query salvata in un file. Per individuare il file è possibile utilizzare la caratteristica di esplorazione disponibile nella procedura guidata, la quale apre automaticamente il file e ne incolla il contenuto nella pagina da cui è stato selezionato il file.  
  
         Se l'origine è un provider [!INCLUDE[vstecado](../../includes/vstecado-md.md)], sarà inoltre possibile utilizzare l'opzione per la copia dei risultati della query specificando la stringa DBCommand come query.  
  
         Se l'origine dati è una vista, l'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la convertirà automaticamente in una tabella nella destinazione.  
  
    -   Indicare se la tabella di destinazione dovrà essere eliminata e quindi ricreata e se consentire IDENTITY_INSERT.  
  
    -   Indicare se eliminare o aggiungere righe a una tabella esistente nella destinazione. Se la tabella non esiste, l'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la creerà automaticamente.  
  
     Se la destinazione è un file flat, è possibile:  
  
    -   Specificare il delimitatore di riga da utilizzare nel file di destinazione.  
  
    -   Specificare il delimitatore di colonna da utilizzare nel file di destinazione.  
  
4.  (Facoltativo) Selezionare una tabella e modificare i mapping tra le colonne di origine e destinazione oppure modificare i metadati delle colonne di destinazione:  
  
    -   Eseguire il mapping delle colonne di origine a colonne di destinazione diverse.  
  
    -   Modificare il tipo di dati delle colonne di destinazione.  
  
    -   Impostare la lunghezza delle colonne con tipi di dati character.  
  
    -   Impostare la precisione e la scala delle colonne con tipi di dati numeric.  
  
    -   Specificare se le colonne possono contenere valori Null.  
  
5.  (Facoltativo) Selezionare più tabelle e aggiornare i metadati e le opzioni da applicarvi:  
  
    -   Selezionare uno schema di destinazione esistente oppure specificare un nuovo schema a cui assegnare le tabelle.  
  
    -   Specificare se abilitare l'opzione IDENTITY_INSERT nelle tabelle di destinazione.  
  
    -   Specificare se eliminare e ricreare le tabelle di destinazione.  
  
    -   Specificare se troncare le tabelle di destinazione esistenti.  
  
6.  Salvare ed eseguire un pacchetto.  
  
     Se la procedura guidata viene avviata da [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o dal prompt dei comandi, il pacchetto potrà essere eseguito immediatamente. È facoltativamente possibile salvare il pacchetto per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **msdb** database o nel file System. Per altre informazioni sul **msdb** del database, vedere [Gestione pacchetti &#40;servizio SSIS&#41;](../service/package-management-ssis-service.md).  
  
     Quando si salva il pacchetto, è possibile impostarne il livello di protezione e, se per quest'ultimo si utilizza una password, specificarla. Per altre informazioni sui livelli di protezione del pacchetto, vedere [controllo di accesso per dati sensibili nei pacchetti](../security/access-control-for-sensitive-data-in-packages.md).  
  
     Se la procedura guidata viene avviata da un progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], non sarà possibile eseguire il pacchetto dalla procedura guidata. Il pacchetto verrà invece aggiunto al progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] da cui è stata avviata la procedura guidata. e potrà quindi essere eseguito in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
    > [!NOTE]  
    >  In [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] l'opzione per salvare il pacchetto creato con la procedura guidata non è disponibile.  
  
## <a name="see-also"></a>Vedere anche  
 [Importazione/Esportazione guidata SQL Server](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)   
 [Creare pacchetti in SQL Server Data Tools](../create-packages-in-sql-server-data-tools.md)  
  
  
