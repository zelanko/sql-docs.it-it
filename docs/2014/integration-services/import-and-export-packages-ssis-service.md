---
title: Importare ed esportare pacchetti (servizio SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], importing
- packages [Integration Services], exporting
- importing packages
- exporting packages
ms.assetid: ef18ec11-b536-47d9-abd1-794099f43486
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9a1d50afde56843942c470017a8534ffa797eb69
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66058145"
---
# <a name="import-and-export-packages-ssis-service"></a>Importare ed esportare pacchetti (servizio SSIS)
    
> [!IMPORTANT]  
>  In questo argomento viene illustrato il servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , un servizio Windows per la gestione dei pacchetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] supporta il servizio per la compatibilità con le versioni precedenti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. A partire da [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], è possibile gestire oggetti come i pacchetti del server Integration Services.  
  
 I pacchetti possono essere salvati nella tabella sysssispackages del database msdb di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o nel file system.  
  
 L'archivio pacchetti, ovvero l'archivio logico gestito e monitorato dal servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , può includere sia il database msdb che le cartelle del file system specificate nel file di configurazione per il servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 È possibile importare ed esportare pacchetti tra i tipi di archivio seguenti:  
  
-   Cartelle del file system in qualsiasi posizione del file system.  
  
-   Cartelle dell'archivio pacchetti SSIS. Le due cartelle predefinite sono File system e MSDB.  
  
-   Il database msdb di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] consente di importare ed esportare pacchetti. Durante queste operazioni il formato e la posizione dei pacchetti vengono modificati. Tramite le caratteristiche di importazione ed esportazione è possibile aggiungere pacchetti al file system, all'archivio pacchetti o al database msdb e copiarli quindi con un formato di archiviazione diverso. I pacchetti salvati in msdb, ad esempio, possono essere copiati nel file system e viceversa.  
  
 È inoltre possibile copiare un pacchetto in un formato diverso tramite l'utilità del prompt dei comandi **dtutil** (dtutil.exe). Per altre informazioni, vedere [dtutil Utility](dtutil-utility.md).  
  
## <a name="to-import-or-export-a-package"></a>Per importare o esportare un pacchetto  
  
> [!IMPORTANT]  
>  In questo argomento viene illustrato il servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che fa parte di [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] supporta il servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] per la compatibilità con le versioni precedenti di [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. Per informazioni sulla gestione dei pacchetti in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], vedere [Integration Services &#40;SSIS&#41; Server](catalog/integration-services-ssis-server-and-catalog.md).  
  
 È possibile importare o esportare un pacchetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] da o nei percorsi seguenti:  
  
-   È possibile importare un pacchetto archiviato in un'istanza di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], nel file System o nell'archivio [!INCLUDE[ssIS](../includes/ssis-md.md)] pacchetti. Il pacchetto importato viene salvato in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o in una cartella nell'archivio pacchetti [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
-   Un pacchetto archiviato nel file system, in un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]o nell'archivio pacchetti [!INCLUDE[ssIS](../includes/ssis-md.md)] può essere esportato in un percorso e un formato di archiviazione diverso.  
  
 Per l'importazione e l'esportazione di un pacchetto tra versioni diverse di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]ci sono tuttavia alcune restrizioni:  
  
-   In un'istanza di [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]è possibile importare pacchetti da un'istanza di [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]ma non è possibile esportare pacchetti in un'istanza di [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)].  
  
-   In un'istanza di [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]non è possibile importare pacchetti da o esportare pacchetti in un'istanza di [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)].  
  
 Le procedure descritte di seguito descrivono come utilizzare [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per importare o esportare un pacchetto.  
  
#### <a name="to-import-a-package-by-using-sql-server-management-studio"></a>Per importare un pacchetto utilizzando SQL Server Management Studio  
  
1.  Fare clic sul pulsante **Start**, scegliere **Microsoft** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e quindi fare clic su **SQL Server Management Studio**.  
  
2.  Nella finestra di dialogo **Connetti al server** impostare le opzioni seguenti:  
  
    -   Nella casella **Tipo server** selezionare **Integration Services**.  
  
    -   Nella casella **nome server** specificare un nome di server oppure fare clic su ** \<Sfoglia per ulteriori informazioni... >** e individuare il server da utilizzare.  
  
3.  Se il riquadro Esplora oggetti non è visualizzato, scegliere **Esplora oggetti** dal menu **Visualizza**.  
  
4.  In Esplora oggetti espandere la cartella **pacchetti archiviati** .  
  
5.  Espandere le sottocartelle per individuare la cartella in cui si desidera importare un pacchetto.  
  
6.  Fare clic con il pulsante destro del mouse sulla cartella e scegliere **Importa pacchetto**, quindi effettuare una delle operazioni seguenti:  
  
    -   Per importare il pacchetto da un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], selezionare l'opzione **SQL Server** , specificare il server e selezionare la modalità di autenticazione. Se si seleziona l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , specificare un nome utente e una password.  
  
         Fare clic sul pulsante Sfoglia **(...)**, selezionare il pacchetto da importare e quindi fare clic su **OK.**  
  
    -   Per importare il pacchetto dal file system, selezionare l'opzione **File system** .  
  
         Fare clic sul pulsante Sfoglia **(...)**, selezionare il pacchetto da importare e quindi fare clic su **Apri.**  
  
    -   Per importare il pacchetto dall'archivio pacchetti [!INCLUDE[ssIS](../includes/ssis-md.md)] , selezionare l'opzione **Archivio pacchetti SSIS** e specificare il server.  
  
         Fare clic sul pulsante Sfoglia **(...)**, selezionare il pacchetto da importare e quindi fare clic su **OK.**  
  
7.  Facoltativamente, aggiornare il nome del pacchetto.  
  
8.  Per aggiornare il livello di protezione del pacchetto, fare clic sul pulsante Sfoglia **(...)** e specificare un livello di protezione diverso usando la finestra di dialogo **Livello di protezione pacchetto**. Se l'opzione **Crittografa tutti i dati sensibili con una password** o **Crittografa tutti i dati con una password** è selezionata, digitare e confermare una password.  
  
9. Fare clic su **OK** per completare l'importazione.  
  
#### <a name="to-export-a-package-by-using-sql-server-management-studio"></a>Per esportare un pacchetto utilizzando SQL Server Management Studio  
  
1.  Fare clic sul pulsante **Start**, scegliere **Microsoft** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e quindi fare clic su **SQL Server Management Studio**.  
  
2.  Nella finestra di dialogo **Connetti al server** impostare le opzioni seguenti:  
  
    -   Nella casella **Tipo server** selezionare **Integration Services**.  
  
    -   Nella casella **nome server** specificare un nome di server oppure fare clic su ** \<Sfoglia per ulteriori informazioni... >** e individuare il server da utilizzare.  
  
3.  Se il riquadro Esplora oggetti non è visualizzato, scegliere **Esplora oggetti** dal menu **Visualizza**.  
  
4.  In Esplora oggetti espandere la cartella **pacchetti archiviati** .  
  
5.  Espandere le sottocartelle per individuare il pacchetto da esportare.  
  
6.  Fare clic sul pacchetto con il pulsante destro del mouse, scegliere **Esporta**e quindi eseguire una delle operazioni seguenti:  
  
    -   Per esportare il pacchetto in un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], selezionare l'opzione **SQL Server** , specificare il server e selezionare la modalità di autenticazione. Se si seleziona l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , specificare un nome utente e una password.  
  
         Fare clic sul pulsante Sfoglia **(...)** ed espandere la cartella **Pacchetti SSIS** per individuare la cartella in cui salvare il pacchetto. Facoltativamente, aggiornare il nome predefinito del pacchetto e quindi scegliere **OK**.  
  
    -   Per esportare il pacchetto nel file system, selezionare l'opzione **File system** .  
  
         Fare clic sul pulsante Sfoglia **(...)** per individuare la cartella in cui esportare il pacchetto, digitare il nome del file del pacchetto e quindi scegliere **Salva**.  
  
    -   Per eseguire l'esportazione nell'archivio pacchetti [!INCLUDE[ssIS](../includes/ssis-md.md)] , selezionare l'opzione **Archivio pacchetti SSIS** e specificare il server.  
  
         Fare clic sul pulsante Sfoglia **(...)**, espandere la cartella **Pacchetti SSIS** e selezionare la cartella in cui si vuole salvare il pacchetto. Facoltativamente, immettere un nuovo nome per il pacchetto nella casella di testo **Nome pacchetto** . [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Per aggiornare il livello di protezione del pacchetto, fare clic sul pulsante Sfoglia **(...)** e specificare un livello di protezione diverso usando la finestra di dialogo **Livello di protezione pacchetto**. Se l'opzione **Crittografa tutti i dati sensibili con una password** o **Crittografa tutti i dati con una password** è selezionata, digitare e confermare una password.  
  
8.  Scegliere **OK** per completare l'esportazione.  
  
## <a name="see-also"></a>Vedi anche  
 [Gestione dei pacchetti &#40;servizio SSIS&#41;](service/package-management-ssis-service.md)  
  
  
