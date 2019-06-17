---
title: Pagina sottoscrizioni personali (gestione Report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 491a85a3-f323-4155-a0a8-de2779899995
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 75d662f677ee2b6bbab8e445804ca7f142b5c034
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108184"
---
# <a name="my-subscriptions-page-report-manager"></a>Pagina Sottoscrizioni personali (Gestione report)
  La pagina Sottoscrizioni personali consente di visualizzare tutte le sottoscrizioni personali in un'unica posizione. Da questa pagina è possibile accedere a tutte le proprie sottoscrizioni, nonché modificarle o eliminarle. L'utente è proprietario solo delle sottoscrizioni che ha creato. Non è possibile accedere alle sottoscrizioni di altri utenti o a sottoscrizioni disponibili per l'utilizzo ma create da altri utenti, ad esempio quando il nome di un utente viene aggiunto a una sottoscrizione esistente definita da un altro utente. Non si possono creare sottoscrizioni da questa pagina. Per altre informazioni sulla creazione di sottoscrizioni, vedere la [pagina nuova sottoscrizione o modifica sottoscrizione &#40;gestione Report&#41;](../../2014/reporting-services/new-subscription-or-edit-subscription-page-report-manager.md).  
  
 Per impostazione predefinita, le sottoscrizioni vengono elencate in ordine alfabetico in base al nome del report. È possibile fare clic su una diversa intestazione di colonna per modificare l'ordinamento delle sottoscrizioni. Se non si è proprietari di sottoscrizioni o se l'autorizzazione per la creazione o la gestione di sottoscrizioni è disabilitata, nella pagina non viene visualizzata alcuna sottoscrizione.  
  
> [!NOTE]  
>  Questa funzionalità non è disponibile in ogni edizione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vedere [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="navigation"></a>Navigazione  
 Utilizzare la procedura riportata di seguito per navigare fino a questo percorso nell'interfaccia utente.  
  
### <a name="to-open-the-my-subscriptions-page"></a>Per aprire la pagina Sottoscrizioni personali  
  
1.  Aprire Gestione report.  
  
2.  Fare clic su Sottoscrizioni personali nell'angolo superiore destro della pagina.  
  
    > [!NOTE]  
    >  La pagina Sottoscrizioni personali è sempre disponibile anche se non si dispone delle autorizzazioni per la creazione di sottoscrizioni.  
  
## <a name="options"></a>Opzioni  
 **Elimina**  
 Selezionare la casella di controllo accanto a ogni sottoscrizione che si desidera eliminare e fare clic su **Elimina**.  
  
 **Modifica**  
 Fare clic per visualizzare o modificare la descrizione.  
  
 **Report**  
 Consente di visualizzare il report specificato nella sottoscrizione. Fare clic sul nome del report per visualizzarlo.  
  
 **Descrizione**  
 Mostra una descrizione della sottoscrizione. Fare clic sulla descrizione per visualizzare o modificare le informazioni sulla sottoscrizione per il report.  
  
 **Cartella**  
 Consente di visualizzare la cartella contenente il report specificato nella sottoscrizione. Fare clic sul nome della cartella per visualizzarne il contenuto.  
  
 **Trigger**  
 Indica i criteri per l'esecuzione della sottoscrizione. Un trigger **TimedSubscription** è basato su una pianificazione che stabilisce quando viene eseguita la sottoscrizione. Un trigger **SnapshotUpdated** è basato sull'aggiornamento di uno snapshot del report.  
  
 **Ultima esecuzione**  
 Mostra la data e ora dell'ultima elaborazione della sottoscrizione.  
  
 **Stato**  
 Mostra lo stato della sottoscrizione. In genere lo stato indica una nuova sottoscrizione o la data e l'ora dell'ultima esecuzione della sottoscrizione.  
  
 Il valore "Dati non validi" indica che la sottoscrizione include un puntatore a valori crittografati non più validi per le credenziali archiviate utilizzate per eseguire il report. I valori crittografati esistenti diventano inutilizzabili quando le chiavi simmetriche utilizzate per crittografare e decrittografare i dati vengono ricreate sul server di report.  
  
 Non è possibile elaborare una sottoscrizione se è stata disattivata. Per aggiornare la sottoscrizione e renderla valida, aprire e salvare la sottoscrizione.  
  
## <a name="see-also"></a>Vedere anche  
 [Sottoscrizioni e recapito &#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Guida sensibile al contesto di Gestione report](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
