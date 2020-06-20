---
title: Selezionare il percorso di destinazione (aggiornamento guidato pacchetti SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.is.upgradewizard.selectdestinationlocation.f1
ms.assetid: 89274a71-0ffe-4889-84df-f5a7d78459ef
author: janinezhang
ms.author: janinez
ms.openlocfilehash: c397e1e174703b40a7bada8ed6fe42675a0c9c24
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84963847"
---
# <a name="select-destination-location-ssis-package-upgrade-wizard"></a>Seleziona posizione di destinazione (Aggiornamento guidato pacchetti SSIS)
  Usare la pagina **Seleziona posizione di destinazione** per specificare la destinazione in cui salvare i pacchetti aggiornati.  
  
> [!NOTE]  
>  Tale pagina è disponibile solo quando si esegue l'Aggiornamento guidato pacchetti [!INCLUDE[ssIS](../includes/ssis-md.md)] da [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] o dal prompt dei comandi.  
  
 **Per eseguire l'Aggiornamento guidato pacchetti SSIS**  
  
-   [Aggiornare i pacchetti di Integration Services mediante l'Aggiornamento guidato pacchetti SSIS](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
## <a name="static-options"></a>Opzioni statiche  
 **Salva in posizione di origine**  
 Consente di salvare i pacchetti aggiornati nella stessa posizione specificata nella pagina **Seleziona posizione di origine** della procedura guidata.  
  
 Se i pacchetti originali sono archiviati nel file system e si desidera eseguire il backup dei pacchetti, selezionare l'opzione **Salva in posizione di origine** . Per altre informazioni, vedere [Aggiornare i pacchetti di Integration Services mediante l'Aggiornamento guidato pacchetti SSIS](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md).  
  
 **Seleziona nuova posizione di destinazione**  
 Consente di salvare i pacchetti aggiornati nella posizione di destinazione specificata nella pagina.  
  
 **Origine pacchetto**  
 Consente di specificare la posizione di archiviazione dei pacchetti di aggiornamento. Per questa opzione sono disponibili i valori elencati nella tabella seguente.  
  
|valore|Description|  
|-----------|-----------------|  
|**File system**|Indica che i pacchetti aggiornati devono essere salvati in una cartella nel computer locale.|  
|**Archivio pacchetti SSIS**|Indica che i pacchetti aggiornati devono essere salvati nell'archivio pacchetti Integration Services. L'archivio pacchetti è costituito dal set di cartelle del file system gestito dal servizio Integration Services. Per altre informazioni, vedere [Gestione dei pacchetti &#40;servizio SSIS&#41;](service/package-management-ssis-service.md).<br /><br /> La selezione di questo valore determina la visualizzazione delle opzioni dinamiche di **Origine pacchetto** corrispondenti.|  
|**Microsoft SQL Server**|Indica che i pacchetti aggiornati devono essere salvati in un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]esistente.<br /><br /> La selezione di questo valore determina la visualizzazione delle opzioni dinamiche di **Origine pacchetto** corrispondenti.|  
  
 **Cartella**  
 Digitare il nome della cartella in cui verranno salvati i pacchetti aggiornati oppure fare clic su **Sfoglia** e individuare la cartella.  
  
 **Sfoglia**  
 Consente di individuare la cartella in cui verranno salvati i pacchetti aggiornati.  
  
## <a name="package-source-dynamic-options"></a>Opzioni dinamiche di Origine pacchetto  
  
### <a name="package-source--ssis-package-store"></a>Origine pacchetto = Archivio pacchetti SSIS  
 **Server**  
 Digitare il nome del server in cui verranno salvati i pacchetti di aggiornamento oppure selezionare un server nell'elenco.  
  
### <a name="package-source--microsoft-sql-server"></a>Origine pacchetto = Microsoft SQL Server  
 **Server**  
 Digitare il nome del server in cui verranno salvati i pacchetti di aggiornamento oppure selezionare il server nell'elenco.  
  
 **Usa autenticazione di Windows**  
 Selezionare questa opzione per utilizzare l'autenticazione di Windows per la connessione al server.  
  
 **Usa autenticazione di SQL Server**  
 Selezionare questa opzione per usare l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per la connessione al server. Se si usa l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , è necessario specificare un nome utente e una password.  
  
 **Nome utente**  
 Digitare il nome utente da usare quando si seleziona l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per la connessione al server.  
  
 **Password**  
 Digitare la password da usare quando si seleziona l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per la connessione al server.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiornare pacchetti di Integration Services](install-windows/upgrade-integration-services-packages.md)  
  
  
