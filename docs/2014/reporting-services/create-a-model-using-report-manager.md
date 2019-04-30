---
title: Creare un modello tramite Gestione Report | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report models [Reporting Services], creating
- Report Manager [Reporting Services], model creation
ms.assetid: 8e5d2bd3-48ec-45f3-afee-6d86797c8f28
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 07865f96b0e4086af346ffc076b1df6d07cda6cd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63265973"
---
# <a name="create-a-model-using-report-manager"></a>Creare un modello tramite Gestione report
  È possibile generare modelli da un cubo di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , da un database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o da un database Oracle utilizzando Gestione report. I modelli di report vengono generati da origini dei dati condivise che vengono pubblicate nel server di report. Se non esiste un'origine dei dati condivisa, è necessario crearla.  
  
 Il modello di report che viene generato si basa interamente sullo schema dell'origine dei dati condivisa. Non è possibile scegliere quali parti dell'origine dei dati includere nel modello, né modificare le regole o i metadati del modello generato. È tuttavia possibile impostare le proprietà del modello dopo che quest'ultimo è stato generato e definire le assegnazioni di ruolo che limitano l'accesso all'intero modello o a parte di esso.  
  
> [!NOTE]  
>  Un modello basato su Oracle generato utilizzando Gestione Report oppure [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[offSPServ](../includes/offspserv-md.md)] 2007 [!INCLUDE[SPS2010](../includes/sps2010-md.md)] includerà oggetti di database che fanno parte dello schema per l'account utente utilizzato per la connessione all'origine dati Oracle. Il nome dell'account utente viene specificato nelle credenziali delle proprietà per l'origine dei dati.  
  
### <a name="to-create-a-new-data-source-for-a-report-model-using-report-manager"></a>Per creare una nuova origine dei dati per un modello di report tramite Gestione report  
  
1.  Digitare l'URL per il server di report nella barra degli indirizzi del browser.  
  
2.  Fare clic su **Nuova origine dati**.  
  
3.  Nella casella di testo **Nome** immettere un nome per l'origine dei dati.  
  
4.  Nella casella di testo **Descrizione** immettere una breve descrizione facoltativa del modello.  
  
5.  Verificare che la casella di controllo **Attiva questa origine dei dati** sia selezionata.  
  
6.  Dalla lista **Tipo di connessione** selezionare il tipo di origine dei dati a cui connettersi. Il tipo di connessione deve essere uno dei seguenti: **Oracle**, **Microsoft SQL Server** oppure **Microsoft SQL Server Analysis Services**.  
  
7.  Nella casella **Stringa di connessione** specificare la stringa di connessione che punta al database.  
  
8.  Selezionare il metodo di connessione che gli utenti di Generatore report dovranno utilizzare per connettersi al database.  
  
    -   Autenticazione di Windows: Selezionare questa opzione quando si desidera che il sistema operativo per eseguire l'autenticazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] agli utenti. Questa opzione consente l'utilizzo in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] delle caratteristiche di sicurezza di Windows, ad esempio la crittografia della password, per l'autenticazione degli utenti. Si consiglia di selezionare questa opzione.  
  
    -   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Autenticazione: Selezionare questa opzione quando si desidera che gli utenti utilizzino un [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] account di accesso è stato creato. Gli utenti dovranno fornire un nome e una password di accesso validi per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
        > [!CAUTION]  
        >  Se possibile, è consigliabile utilizzare l'autenticazione di Windows.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-create-a-report-model-using-report-manager"></a>Per creare un modello di report tramite Gestione report  
  
1.  In Gestione report selezionare l'origine dei dati che si desidera utilizzare per il modello.  
  
     Verrà visualizzata la pagina Proprietà.  
  
2.  Verificare quali opzioni si intende utilizzare per l'origine dei dati.  
  
3.  Fare clic su **Genera modello**.  
  
     Verrà visualizzata la pagina Generale per l'origine dei dati.  
  
4.  Nella casella di testo **Nome** immettere un nome per il modello di report.  
  
5.  Nella casella **Descrizione** immettere una breve descrizione del modello.  
  
6.  Per specificare un nuovo percorso in cui salvare il modello di report fare clic su **Cambia percorso**.  
  
     Per impostazione predefinita, il modello di report viene salvato nella cartella Home di Gestione report.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     Il modello di report verrà creato e salvato nel percorso specificato. È possibile assegnare autorizzazioni a questo modello utilizzando Gestione report.  
  
## <a name="see-also"></a>Vedere anche  
 [Concessione di autorizzazioni in un server di report in modalità nativa](security/granting-permissions-on-a-native-mode-report-server.md)   
 [Connessioni dati, origini dati e stringhe di connessione in Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Pagina Nuova origine dati &#40;Gestione report&#41;](../../2014/reporting-services/new-data-source-page-report-manager.md)  
  
  
