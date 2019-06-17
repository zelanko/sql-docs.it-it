---
title: SQL Server importazione / esportazione guidata | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- exporting data
- mapping files [Integration Services]
- SQL Server Import and Export Wizard
- SSIS packages, creating
- packages [Integration Services], copying
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
- Import and Export Wizard
- copying data [Integration Services]
- importing data, SSIS packages
- sources [Integration Services], copying data
ms.assetid: c0e4d867-b2a9-4b2a-844b-2fe45be88f81
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2f3ce90e2670357d0842b0a6ac7838f396465bab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768165"
---
# <a name="sql-server-import-and-export-wizard"></a>Importazione/Esportazione guidata SQL Server
  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] importazione / esportazione guidata offre il metodo più semplice per creare un [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pacchetto che copia i dati da un'origine a una destinazione.  
  
> [!NOTE]  
>  In un computer a 64 bit con [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] viene installata la versione a 64 bit dell'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (DTSWizard.exe). Tuttavia, alcune origini dati, ad esempio Access o Excel, dispongono solo di un provider a 32 bit. Per utilizzare queste origini dati, potrebbe essere necessario installare ed eseguire la versione a 32 bit della procedura guidata. Per installare la versione a 32 bit della procedura guidata, selezionare gli strumenti client o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] durante l'installazione.  
  
 È possibile avviare l'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dal menu Start, da [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], da [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o dal prompt dei comandi. Per altre informazioni, vedere [esecuzione di SQL Server importazione / esportazione guidata](start-the-sql-server-import-and-export-wizard.md).  
  
 L'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente di copiare dati in e da qualsiasi origine dati per cui sia disponibile un provider di dati [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] gestito o un provider OLE DB nativo. L'elenco dei provider disponibili include le origini dati seguenti:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   File flat  
  
-   Microsoft Office Access  
  
-   Microsoft Office Excel  
  
 Alcune caratteristiche della procedura guidata funzionano in modo diverso a seconda dell'ambiente da cui la procedura viene avviata.  
  
-   Se si avvia il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] importazione / esportazione guidata [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], si esegue il pacchetto immediatamente, selezionando il **vengono eseguite immediatamente** casella di controllo. Per impostazione predefinita, questa casella di controllo è selezionata e il pacchetto viene immediatamente eseguito.  
  
     È inoltre possibile decidere se salvare il pacchetto in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o nel file system. Se si decide di salvare il pacchetto, è inoltre necessario specificare un livello di protezione. Per altre informazioni sui livelli di protezione del pacchetto, vedere [controllo di accesso per dati sensibili nei pacchetti](../security/access-control-for-sensitive-data-in-packages.md).  
  
     Dopo la creazione del pacchetto nell'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e la copia dei dati, è possibile utilizzare Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] per aprire e modificare il pacchetto salvato aggiungendo attività, trasformazioni e logica guidata dagli eventi.  
  
    > [!NOTE]  
    >  In [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] l'opzione per salvare il pacchetto creato con la procedura guidata non è disponibile.  
  
-   Se si avvia Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da un progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], non sarà possibile eseguire il pacchetto durante un passaggio della procedura guidata. Il pacchetto verrà invece aggiunto al progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] da cui è stata avviata la procedura guidata. Sarà quindi possibile eseguire il pacchetto o estenderlo aggiungendo attività, trasformazioni e logica guidata dagli eventi utilizzando Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)].  
  
 Per altre informazioni, vedere [esecuzione di SQL Server importazione / esportazione guidata](start-the-sql-server-import-and-export-wizard.md).  
  
## <a name="permissions-required-by-the-import-and-export-wizard"></a>Autorizzazioni richieste dall'Importazione/Esportazione guidata  
 Per completare l'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario disporre almeno delle autorizzazioni seguenti:  
  
-   Autorizzazioni per la connessione alle condivisioni file o ai database di origine e di destinazione. A tale scopo, in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sono necessari diritti di accesso al server e al database.  
  
-   Autorizzazioni per la lettura dei dati dal file o dal database di origine. A tale scopo, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono necessarie le autorizzazioni SELECT nelle viste e nelle tabelle di origine.  
  
-   Autorizzazioni per la scrittura dei dati nel file o nel database di destinazione. A tale scopo, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono necessarie le autorizzazioni INSERT nelle tabelle di destinazione.  
  
-   Se si desidera creare un nuovo file, tabella o database di destinazione, autorizzazioni sufficienti per creare il nuovo file, tabella o database. A tale scopo, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono necessarie le autorizzazioni CREATE DATABASE o CREATE TABLE.  
  
-   Se si desidera salvare il pacchetto creato dalla procedura guidata, autorizzazioni sufficienti per scrivere nel database msdb o nel file System. In [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], questo richiede l'autorizzazione INSERT nel database msdb.  
  
## <a name="mapping-data-types-in-the-import-and-export-wizard"></a>Esecuzione del mapping di tipi di dati nell'Importazione/Esportazione guidata  
 Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offre solo le funzionalità di trasformazione di base. Ad eccezione dell'impostazione del nome, del tipo di dati e delle proprietà del tipo di dati delle colonne incluse nei nuovi file e tabelle di destinazione, l'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non supporta trasformazioni a livello di colonna.  
  
 Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizza i file di mapping disponibili in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per eseguire il mapping dei tipi di dati da una versione o un sistema di database a un'altro. È ad esempio possibile eseguire il mapping da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a Oracle. I file di mapping in formato XML vengono installati per impostazione predefinita in C:\Programmi\Microsoft SQL Server\100\DTS\MappingFiles. Se sono necessari tipi di mapping diversi tra i tipi di dati, sarà possibile aggiornare i file di mapping per modificare come desiderato i mapping eseguiti dalla procedura guidata. Ad esempio, se si desidera che il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **nchar** tipo di dati per eseguire il mapping a DB2 **GRAPHIC** tipo di dati anziché DB2 **VARGRAPHIC** del tipo di dati durante il trasferimento dei dati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a DB2, è possibile modificare il **nchar** mapping nel file di mapping SqlClientToIBMDB2.xml usare **GRAPHIC** anziché **VARGRAPHIC.**  
  
 In [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sono inclusi mapping tra le combinazioni di origini e destinazioni maggiormente utilizzate ed è possibile aggiungere nuovi file di mapping alla directory MappingFiles per supportare ulteriori origini e destinazioni. I nuovi file di mapping devono essere conformi allo schema XSD pubblicato ed eseguire il mapping tra una combinazione univoca di origine e destinazione.  
  
> [!NOTE]  
>  Se si modifica un file di mapping esistente o si aggiunge un nuovo file di mapping alla cartella, affinché i file nuovi o modificati vengano riconosciuti, è necessario chiudere e riaprire l'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
## <a name="external-resources"></a>Risorse esterne  
  
-   Video [esportazione di dati di SQL Server in Excel (Video di SQL Server)](https://go.microsoft.com/fwlink/?LinkID=200975), su technet.microsoft.com  
  
-   Esempio di CodePlex [esportazione da ODBC in un File Flat tramite una procedura guidata: Pacchetti di lezioni](https://go.microsoft.com/fwlink/?LinkId=217657), su msftisprodsamples.codeplex.com  
  
  
