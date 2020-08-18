---
description: Salva pacchetto SSIS (Importazione/Esportazione guidata SQL Server)
title: Salvare il pacchetto SSIS (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.savedtspackage.f1
ms.assetid: 7bf8ac6a-5599-43ab-bf5c-e072c11b85a0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 379973cb0174e25a91b6a3dfb0ed7cc319efd842
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88346817"
---
# <a name="save-ssis-package-sql-server-import-and-export-wizard"></a>Salva pacchetto SSIS (Importazione/Esportazione guidata SQL Server)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Se nella pagina **Salvare ed eseguire il pacchetto** l'utente ha specificato di voler salvare le proprie impostazioni come pacchetto di SQL Server Integration Services (SSIS), l'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] visualizza **Salva pacchetto SSIS**. In questa pagina è necessario specificare opzioni aggiuntive per il salvataggio del pacchetto creato dalla procedura guidata.  

Le opzioni presenti nella pagina **Salva pacchetto SSIS** dipendono dalle scelte effettuate in precedenza nella pagina **Salvare ed eseguire il pacchetto** per salvare il pacchetto in SQL Server o nel file system. Per esaminare di nuovo la pagina **Salvare ed eseguire il pacchetto** , vedere [Salvare ed eseguire il pacchetto](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).
 
**Cos'è un pacchetto?** La procedura guidata usa SQL Server Integration Services (SSIS) per copiare i dati. In SSIS il pacchetto rappresenta l'unità di base. La procedura guidata crea un pacchetto SSIS in memoria mentre ci si sposta tra le pagine della procedura guidata e si specificano le opzioni.

## <a name="screen-shot---common-options"></a>Schermata - Opzioni comuni
L'immagine seguente illustra la prima parte della pagina **Salva pacchetto SSIS** della procedura guidata. Il resto della pagina presenta un numero variabile di opzioni che variano a seconda della destinazione del pacchetto scelta.

![Salva pacchetto - Opzioni comuni](../../integration-services/import-export-data/media/save-package-common-options.png)

## <a name="provide-a-name-and-description-for-the-package"></a>Specificare un nome e una descrizione per il pacchetto  
 **Nome**  
 Consente di specificare un nome univoco per il pacchetto.  
  
 **Descrizione**  
 Consente di specificare una descrizione per il pacchetto. È consigliabile descrivere gli scopi del pacchetto, in modo da ottenere pacchetti autodocumentati più semplici da gestire.  
  
 **Destinazione**  
 La destinazione ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o file system) specificata in precedenza per il pacchetto. Per salvare il pacchetto in un'altra destinazione, tornare alla pagina **Salvare ed eseguire il pacchetto** .

## <a name="screen-shot---save-the-package-in-sql-server"></a>Screenshot del salvataggio del pacchetto in SQL Server

 L'immagine seguente illustra la pagina **Salva pacchetto SSIS** della procedura guidata se è stata selezionata l'opzione **SQL Server** nella pagina **Salvare ed eseguire il pacchetto**. 
  
![Pagina Salva pacchetto SSIS dell'Importazione/Esportazione guidata](../../integration-services/import-export-data/media/save-package2.png "Pagina Salva pacchetto SSIS dell'Importazione/Esportazione guidata")  

## <a name="options-to-specify-target--sql-server"></a>Opzioni da specificare (destinazione = SQL Server) 

 > [!NOTE]
 > La procedura guidata salva il pacchetto nel database **msdb** nella tabella **sysssispackages**. Questa opzione **non** salva il pacchetto nel database del catalogo SSIS (SSISDB).  
 
 **Nome server**  
 Digitare o selezionare il nome del server di destinazione.  
   
 **Usa autenticazione di Windows**  
Connettersi al server tramite l'autenticazione integrata di Windows. Questo è il metodo di autenticazione ottimale.  
  
 **Usa autenticazione di SQL Server**  
Connettersi al server tramite l'autenticazione di SQL Server.  
  
 **Nome utente**  
Se è stata specificata l'autenticazione di SQL Server, immettere il nome utente.  
  
 **Password**  
Se è stata specificata l'autenticazione di SQL Server, immettere la password.  
    
## <a name="screen-shot---save-the-package-in-the-file-system"></a>Screenshot del salvataggio del pacchetto nel file system
 
L'immagine seguente illustra la pagina **Salva pacchetto SSIS** della procedura guidata se è stata selezionata l'opzione **File system** nella pagina **Salvare ed eseguire il pacchetto**. 
  
![Pagina Salva pacchetto SSIS dell'Importazione/Esportazione guidata](../../integration-services/import-export-data/media/save-package1.png "Pagina Salva pacchetto SSIS dell'Importazione/Esportazione guidata")  

## <a name="options-to-specify-target--file-system"></a>Opzioni da specificare (destinazione = file system)

 **Nome file**  
 Immettere il percorso e il nome del file di destinazione. In alternativa usare il pulsante **Sfoglia** per selezionare una destinazione.  
  
> [!TIP]
> Assicurarsi di specificare una cartella di destinazione, digitandola o sfogliandola. Se si immette solo il nome del file senza percorso, l'utente non saprà la destinazione in cui la procedura guidata salverà il pacchetto. Inoltre, la procedura guidata potrebbe provare a salvare il pacchetto in un percorso di cui non dispone dell'autorizzazione per il salvataggio dei file e generare un errore.  
>   
>  Tenere presente la destinazione di salvataggio del file del pacchetto.  
  
 **Sfoglia**  
 Facoltativamente usare la funzione Sfoglia per selezionare il percorso del file di destinazione nella finestra di dialogo **Salvataggio pacchetto**.  

## <a name="about-the-two-pages-of-options-for-saving-the-package"></a>Informazioni sulle due pagine di opzioni per il salvataggio del pacchetto  
 La pagina **Salva pacchetto SSIS** è una delle due pagine in cui è possibile selezionare le opzioni per il salvataggio del pacchetto SSIS.  
  
-   Nella pagina precedente, **Salvare ed eseguire il pacchetto**, è possibile scegliere di salvare il pacchetto in SQL Server o come file. È anche possibile selezionare le impostazioni di protezione per il pacchetto salvato. Per esaminare di nuovo la pagina **Salvare ed eseguire il pacchetto** , vedere [Salvare ed eseguire il pacchetto](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).  
  
-   Nella pagina corrente è possibile assegnare un nome al pacchetto e definire altre informazioni sulla posizione in cui salvarlo.  
 
## <a name="run-the-saved-package-again-later"></a>Esecuzione del pacchetto salvato in un secondo momento  
 Per informazioni su come eseguire il pacchetto salvato in un secondo momento, vedere uno gli argomenti seguenti.  
  
-   Per eseguire un pacchetto usando un'utilità con interfaccia utente semplice da usare, vedere [Guida di riferimento dell'interfaccia utente di Utilità di esecuzione pacchetti &#40;DtExecUI&#41;](../../integration-services/packages/execute-package-utility-dtexecui-ui-reference.md).  
  
-   Per eseguire un pacchetto dalla riga di comando o da un file batch, vedere [Utilità dtexec](../../integration-services/packages/dtexec-utility.md).  
  
-   Se il pacchetto è stato salvato in SQL Server nel database **msdb** , connettersi al servizio Integration Services. In SQL Server Management Studio, in Esplora oggetti accedere a **Pacchetti archiviati | MSDB**, fare clic con il pulsante destro del mouse sul pacchetto e selezionare **Esegui pacchetto**.

-   Se il pacchetto è stato salvato nel file system, vedere [Eseguire pacchetti di Integration Services (SSIS)](../../integration-services/packages/run-integration-services-ssis-packages.md) per eseguire il pacchetto nell'ambiente di sviluppo. È necessario aggiungere il pacchetto a un progetto di Integration Services prima di poterlo aprire ed eseguire.  

## <a name="customize-the-saved-package"></a>Personalizzazione del pacchetto salvato  
 Per informazioni su come personalizzare il pacchetto salvato, vedere [Pacchetti di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-packages.md).  
  
## <a name="whats-next"></a>Passaggi successivi  
 Dopo aver specificato le opzioni aggiuntive per il salvataggio del pacchetto, la pagina successiva è **Completare la procedura guidata**. In questa pagina è possibile rivedere le scelte effettuate nella procedura guidata, quindi di avviare l'operazione. Per altre informazioni, vedere [Completare la procedura guidata](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md).  
 
## <a name="see-also"></a>Vedere anche  
[Salvataggio di pacchetti](../../integration-services/save-packages.md)  
[Eseguire pacchetti di Integration Services (SSIS)](../../integration-services/packages/run-integration-services-ssis-packages.md)  
[SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)
 
 
