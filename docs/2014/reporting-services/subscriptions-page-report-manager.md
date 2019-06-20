---
title: Pagina sottoscrizioni (gestione Report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: cf3a6bd0-e0b2-4875-a532-63ef34cfa860
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: eec92d7c58b68b14374666f65489f145fa863422
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66101092"
---
# <a name="subscriptions-page-report-manager"></a>Pagina Sottoscrizioni (Gestione report)
  La pagina Sottoscrizioni consente di visualizzare un elenco di tutte le sottoscrizioni del report o dell'origine dati condivisa corrente. Se sono disponibili autorizzazioni sufficienti (quelle assegnate dall'attività Gestione di tutte le sottoscrizioni) è possibile visualizzare le sottoscrizioni di tutti gli utenti. In caso contrario, in questa pagina vengono visualizzate solo le sottoscrizioni personali.  
  
> [!NOTE]  
>  Le informazioni sulle sottoscrizioni sono disponibili anche in altre pagine. Per altre informazioni, vedere [pagina sottoscrizioni personali &#40;gestione Report&#41; ](../../2014/reporting-services/my-subscriptions-page-report-manager.md) per accedere a tutte le sottoscrizioni in un'unica posizione o il [pagina nuova sottoscrizione o modifica sottoscrizione &#40;gestione Report&#41; ](../../2014/reporting-services/new-subscription-or-edit-subscription-page-report-manager.md) per creare o modificare una sottoscrizione.  
  
 Alcune opzioni sono disponibili solo in presenza di sottoscrizioni esistenti. Se non esistono sottoscrizioni definite e si accede a questa pagina da un report, saranno disponibili solo i pulsanti **Nuova sottoscrizione** e **Nuova sottoscrizione guidata dai dati** .  
  
 Prima di creare una nuova sottoscrizione, è necessario verificare che l'origine dati del report utilizzi credenziali archiviate. Per archiviare le credenziali, utilizzare la pagina delle proprietà Origini dati. Per altre informazioni, vedere [pagina delle proprietà origini dati &#40;gestione Report&#41;](../../2014/reporting-services/data-sources-properties-page-report-manager.md).  
  
> [!NOTE]  
>  Questa funzionalità non è disponibile in ogni edizione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vedere [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="navigation"></a>Navigazione  
 Utilizzare la procedura riportata di seguito per navigare fino a questo percorso nell'interfaccia utente.  
  
### <a name="to-open-the-subscriptions-page-for-report"></a>Per aprire la pagina Sottoscrizioni per il report  
  
1.  Aprire Gestione report, quindi individuare il report per il quale si desidera visualizzare o configurare una sottoscrizione.  
  
2.  Passare con il puntatore del mouse sul report, quindi fare clic sulla freccia a discesa.  
  
3.  Scegliere **Gestisci**dal menu a discesa. Verrà visualizzata la pagina delle proprietà Generale per il report.  
  
4.  Selezionare la scheda **Sottoscrizioni** .  
  
## <a name="options"></a>Opzioni  
 **Elimina**  
 Fare clic per eliminare una sottoscrizione. Prima di poter eliminare una sottoscrizione è necessario selezionare la casella di controllo accanto a ogni sottoscrizione che si desidera eliminare.  
  
 **Nuova sottoscrizione**  
 Fare clic per creare una nuova sottoscrizione del report corrente. Questo pulsante è abilitato quando il report utilizza credenziali archiviate o non utilizza credenziali. Questo pulsante non è disponibile quando si accede alla pagina Sottoscrizioni per un'origine dati condivisa.  
  
 **Nuova sottoscrizione guidata dai dati**  
 Fare clic per generare un elenco di Sottoscrittori e di opzioni di recapito da un comando o da una query su un archivio dati contenente tali informazioni. Questo pulsante è abilitato quando il report utilizza credenziali archiviate o non utilizza credenziali. Questo pulsante non è disponibile quando si accede alla pagina Sottoscrizioni per un'origine dati condivisa.  
  
 **Modifica**  
 Fare clic per visualizzare o modificare la descrizione.  
  
 **Report**  
 Quando si apre la pagina da un'origine dati condivisa, questa colonna indica il report per cui è stata definita la sottoscrizione. Nella colonna **Cartella** è indicato il percorso del report.  
  
 **Descrizione**  
 Mostra una descrizione della sottoscrizione.  
  
 **Trigger**  
 Indica i criteri per l'esecuzione della sottoscrizione. Un trigger **TimedSubscription** è basato su una pianificazione che stabilisce quando viene eseguita la sottoscrizione. Un trigger **SnapshotUpdated** è basato sull'aggiornamento di uno snapshot del report.  
  
 **Proprietario**  
 Mostra il nome dell'utente che ha creato la sottoscrizione.  
  
 **Ultima esecuzione**  
 Mostra la data e ora dell'ultima elaborazione della sottoscrizione.  
  
 **Stato**  
 Mostra lo stato della sottoscrizione. In genere il valore dello stato corrisponde a Nuovo oppure alla data e ora dell'ultima esecuzione della sottoscrizione.  
  
 Il valore "Dati non validi" indica che la sottoscrizione include un puntatore a valori crittografati non più validi per le credenziali archiviate utilizzate per eseguire il report. I valori crittografati esistenti diventano inutilizzabili quando le chiavi simmetriche utilizzate per crittografare e decrittografare i dati vengono ricreate sul server di report.  
  
 Non è possibile elaborare una sottoscrizione se è stata disattivata. Per aggiornare la sottoscrizione e renderla valida, aprire e salvare la sottoscrizione.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione report &#40;modalità nativa SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Creare, modificare ed eliminare sottoscrizioni Standard &#40;Reporting Services in modalità nativa&#41;](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)   
 [Create, Modify, and Delete Schedules](subscriptions/create-modify-and-delete-schedules.md)   
 [Guida sensibile al contesto di Gestione report](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
