---
title: Salvare ed eseguire il pacchetto (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.saveschedule.f1
ms.assetid: b582c462-3d7a-4a4c-a2a2-2c79fedab75a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8326920e557d6ed304414f96a7da040de0093dd0
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/16/2019
ms.locfileid: "65723729"
---
# <a name="save-and-run-package-sql-server-import-and-export-wizard"></a>Salvare ed eseguire il pacchetto (Importazione/Esportazione guidata SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Dopo aver specificato e configurato l'origine dati e la destinazione, l'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostra **Salvare ed eseguire il pacchetto**. In questa pagina specificare se eseguire immediatamente l'operazione di copia. A seconda della configurazione, è anche possibile salvare le proprie informazioni come pacchetto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS) per personalizzarlo e usarlo di nuovo in seguito.
  
**Cos'è un pacchetto?** La procedura guidata usa SQL Server Integration Services (SSIS) per copiare i dati. In SSIS il pacchetto rappresenta l'unità di base. La procedura guidata crea un pacchetto SSIS in memoria mentre ci si sposta tra le pagine della procedura guidata e si specificano le opzioni.
  
## <a name="screen-shot-of-the-save-and-run-package-page"></a>Screenshot della pagina Salvare ed eseguire il pacchetto  
L'immagine seguente illustra la pagina **Salvare ed eseguire il pacchetto** della procedura guidata. 
   
![Pagina Salva ed esegui pacchetto dell'Importazione/Esportazione guidata](../../integration-services/import-export-data/media/save-and-run.png "Pagina Salva ed esegui pacchetto dell'Importazione/Esportazione guidata") 
  
## <a name="run-and-save-the-package"></a>Eseguire e salvare il pacchetto 
 Per continuare è necessario selezionare almeno una delle due opzioni seguenti.  
  
 **Run immediately**  
 Selezionare questa opzione per importare ed esportare i dati immediatamente. Per impostazione predefinita, questa casella di controllo è selezionata e l'operazione viene immediatamente eseguita.
  
 **Salva pacchetto SSIS**  
 Salvare le impostazioni come un pacchetto SSIS. In un secondo momento è facoltativamente possibile personalizzare il pacchetto ed eseguirlo nuovamente. Se si sceglie di salvare il pacchetto, sono disponibili opzioni aggiuntive nella pagina successiva, **Salva pacchetto SSIS**.
 
L'opzione per salvare il pacchetto è disponibile solo se si usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard Edition o un'edizione superiore.   
  
> [!NOTE]
> Se si completa la procedura guidata, si esegue l'operazione ma la si interrompe prima del completamento, il pacchetto non viene salvato, anche se si seleziona la casella di controllo **Salva pacchetto SSIS** in questa pagina.  

### <a name="if-you-started-the-wizard-from-visual-studio"></a>Se la procedura guidata è stata avviata da Visual Studio
Se la procedura guidata è stata avviata da un progetto di Integration Services in Visual Studio con SQL Server Data Tools (SSDT):
-   Non è possibile **eseguire** il pacchetto se non dopo aver chiuso la procedura guidata. È quindi possibile eseguire il pacchetto da Visual Studio.
-   La procedura guidata **salva** il pacchetto nel progetto di Integration Services da cui la procedura è stata avviata.

## <a name="specify-options-for-saving-the-package"></a>Specificare le opzioni di salvataggio del pacchetto
**SQL Server**  
 Selezionare questa opzione per salvare il pacchetto in SQL Server nel database **msdb** nella tabella **sysssispackages**.
 
> [!IMPORTANT]
> Questa opzione non salva il pacchetto nel database del catalogo SSIS (SSISDB).  

 È possibile selezionare il server di destinazione e fornire le credenziali per connettersi al server nella pagina successiva, **Salva pacchetto SSIS**. Per altre informazioni, vedere [Salva pacchetto SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
  
 **File system**  
 Selezionare questa opzione per salvare il pacchetto come file con estensione **dtsx**.  
  
 È possibile selezionare la cartella e il nome file di destinazione per il pacchetto nella pagina successiva, **Salva pacchetto SSIS**. Per altre informazioni, vedere [Salva pacchetto SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
 
 ## <a name="specify-the-package-protection-level"></a>Specificare il livello di protezione del pacchetto
 **Livello di protezione pacchetto**  
 Selezionare un livello di protezione dall'elenco per proteggere i dati nel pacchetto.  
  
 Il livello di protezione determina il metodo di protezione, la password o chiave utente e l'ambito di protezione del pacchetto. La protezione può includere tutti i dati o solo i dati sensibili. Per altre informazioni sulle opzioni disponibili, vedere [Access Control for Sensitive Data in Packages](../../integration-services/security/access-control-for-sensitive-data-in-packages.md).  
  
 **Password**  
 Digitare una password.  
  
 **Conferma password**  
 Digitare di nuovo la password.  
  
> [!NOTE]
> Le opzioni per la password sono disponibili solo se viene specificato un **Livello di protezione pacchetto** che richiede una password, ovvero se si specifica **Crittografa tutti i dati sensibili con una password** o **Crittografa tutti i dati con una password**.  

## <a name="about-the-two-pages-of-options-for-saving-the-package"></a>Informazioni sulle due pagine di opzioni per il salvataggio del pacchetto  
 La pagina **Salvare ed eseguire il pacchetto** è una delle due pagine in cui è possibile selezionare le opzioni per il salvataggio del pacchetto SSIS.  
  
-   Nella pagina corrente è possibile scegliere di salvare il pacchetto in SQL Server o come file. È anche possibile selezionare le impostazioni di protezione per il pacchetto salvato.  
  
-   Quindi, nella pagina **Salva pacchetto SSIS** è possibile assegnare un nome al pacchetto e definire altre informazioni sulla posizione in cui salvarlo. Per altre informazioni, vedere [Salva pacchetto SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
  
 Queste opzioni sono disponibili solo se si seleziona l'opzione **Salva pacchetto SSIS** in questa pagina.  
  
## <a name="whats-next"></a>Quali sono le operazioni successive?  
 Dopo aver specificato se eseguire immediatamente l'operazione di copia e se si desidera salvare il pacchetto, la pagina successiva dipende dalle opzioni scelte.  
  
-   Se è stata selezionata l'opzione per eseguire il pacchetto immediatamente ma senza salvarlo, la pagina successiva è **Completamento procedura guidata**. In questa pagina è possibile rivedere le scelte effettuate nella procedura guidata e quindi avviare l'operazione di copia. Per altre informazioni, vedere [Completare la procedura guidata](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md).  
  
-   Se è stata seleziona l'opzione per salvare il pacchetto, la pagina successiva è **Salva pacchetto SSIS**. In questa pagina è necessario specificare opzioni aggiuntive per il salvataggio del pacchetto. Quindi, dopo aver salvato il pacchetto, la pagina successiva è **Completamento procedura guidata**. Per altre informazioni, vedere [Salva pacchetto SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
  
## <a name="see-also"></a>Vedere anche  
[Salvare i pacchetti](../../integration-services/save-packages.md)  
[Eseguire pacchetti di Integration Services (SSIS)](../../integration-services/packages/run-integration-services-ssis-packages.md)  
[SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
[Iniziare con questo semplice esempio dell'Importazione/Esportazione guidata](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

  

