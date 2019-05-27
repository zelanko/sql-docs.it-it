---
title: Selezionare il percorso di origine (aggiornamento guidato pacchetti SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.is.upgradewizard.selectsourcelocation.f1
ms.assetid: 429f146e-edb4-4401-a225-f2c8468971c5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1ba348d3a47945bf9bb4f375310c5c92e6be7705
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66055937"
---
# <a name="select-source-location-ssis-package-upgrade-wizard"></a>Seleziona posizione di origine (Aggiornamento guidato pacchetti SSIS)
  Usare la pagina **Seleziona posizione di origine** per specificare l'origine da cui eseguire l'aggiornamento dei pacchetti.  
  
> [!NOTE]  
>  Tale pagina è disponibile solo quando si esegue l'Aggiornamento guidato pacchetti [!INCLUDE[ssIS](../includes/ssis-md.md)] da [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] o dal prompt dei comandi.  
  
 **Per eseguire l'Aggiornamento guidato pacchetti SSIS**  
  
-   [Aggiornare i pacchetti di Integration Services mediante l'Aggiornamento guidato pacchetti SSIS](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
## <a name="static-options"></a>Opzioni statiche  
 **Origine pacchetto**  
 Selezionare il percorso di archiviazione che contiene i pacchetti da aggiornare. Per questa opzione sono disponibili i valori elencati nella tabella seguente.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**File System**|Indica che i pacchetti da aggiornare si trovano in una cartella nel computer locale.<br /><br /> Per eseguire il backup dei pacchetti originali prima dell'aggiornamento, è necessario archiviare i pacchetti originali nel file system. Per ulteriori informazioni, vedere l'argomento relativo alla procedura.|  
|**Archivio pacchetti SSIS**|Indica che i pacchetti da aggiornare si trovano nell'archivio pacchetti. L'archivio pacchetti è costituito dal set di cartelle del file system gestito dal servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Per altre informazioni, vedere [Gestione dei pacchetti &#40;servizio SSIS&#41;](service/package-management-ssis-service.md).<br /><br /> La selezione di questo valore determina la visualizzazione delle opzioni dinamiche di **Origine pacchetto** corrispondenti.|  
|**Microsoft SQL Server**|Indica che i pacchetti da aggiornare provengono da un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]esistente.<br /><br /> La selezione di questo valore determina la visualizzazione delle opzioni dinamiche di **Origine pacchetto** corrispondenti.|  
  
 **Cartella**  
 Digitare il nome di una cartella che contiene i pacchetti da aggiornare o fare clic su **Sfoglia** e individuare la cartella.  
  
 **Sfoglia**  
 Consente di individuare la cartella che contiene i pacchetti da aggiornare.  
  
## <a name="package-source-dynamic-options"></a>Opzioni dinamiche di Origine pacchetto  
  
### <a name="package-source--ssis-package-store"></a>Origine pacchetto = Archivio pacchetti SSIS  
 **Server**  
 Digitare il nome del server che contiene i pacchetti da aggiornare oppure selezionare il server nell'elenco.  
  
### <a name="package-source--microsoft-sql-server"></a>Origine pacchetto = Microsoft SQL Server  
 **Server**  
 Digitare il nome del server che contiene i pacchetti da aggiornare oppure selezionare il server dall'elenco.  
  
 **Usa autenticazione di Windows**  
 Selezionare questa opzione per utilizzare l'autenticazione di Windows per la connessione al server.  
  
 **Usa autenticazione di SQL Server**  
 Selezionare questa opzione per usare l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per la connessione al server. Se si usa l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , è necessario specificare un nome utente e una password.  
  
 **Nome utente**  
 Digitare il nome utente usato dall'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per la connessione al server.  
  
 **Password**  
 Digitare la password usata dall'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per la connessione al server.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiornare pacchetti di Integration Services](install-windows/upgrade-integration-services-packages.md)  
  
  
