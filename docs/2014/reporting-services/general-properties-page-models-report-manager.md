---
title: Pagina delle proprietà generale, modelli (gestione Report) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.modelproperties.general.f1
ms.assetid: 7ad59850-8135-4c4d-95e9-6d705b6d77a8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2523909f2719fb8316acecf8ad0b56ddbe086a36
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63260813"
---
# <a name="general-properties-page-models-report-manager"></a>Pagina delle proprietà Generale, Modelli (Gestione report)
  La pagina delle proprietà Generale per i modelli di report consente di rinominare, eliminare, spostare o sostituire il file di definizione del modello, con estensione smdl. Nella parte superiore della pagina vengono visualizzati il nome dell'utente che ha creato o modificato il modello e la data e ora di creazione o modifica.  
  
## <a name="navigation"></a>Navigazione  
 Utilizzare la procedura riportata di seguito per navigare fino a questo percorso nell'interfaccia utente.  
  
###### <a name="to-open-the-general-properties-page-for-a-model"></a>Per aprire la pagina delle proprietà Generale per un modello.  
  
1.  Aprire Gestione report, quindi individuare il modello per il quale si desidera visualizzare o configurare le proprietà.  
  
2.  Passare con il puntatore del mouse sul modello, quindi fare clic sulla freccia a discesa.  
  
3.  Scegliere **Gestisci**dal menu a discesa. Verrà visualizzata la pagina delle proprietà Generale per il modello.  
  
## <a name="options"></a>Opzioni  
 **Name**  
 Consente di specificare il nome del modello. Il nome deve includere almeno un carattere alfanumerico. È inoltre possibile utilizzare spazi e alcuni simboli. Il nome non può contenere i caratteri seguenti:  
  
 ; ? : \@ & = + , $ / * \< > | " /  
  
 **Descrizione**  
 Indica una descrizione del modello. Questa descrizione viene visualizzata nella pagina Contenuto per gli utenti autorizzati ad accedere al modello.  
  
 **Nascondi in visualizzazione elenco**  
 Selezionare questa casella di controllo per nascondere l'elemento quando è impostata la visualizzazione Elenco per la cartella. La visualizzazione Elenco rappresenta una modalità di visualizzazione per il contenuto delle cartelle supportata in Gestione report. È possibile impostare questa opzione in [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] per definire la modalità di visualizzazione di questo elemento in Gestione report. Per altre informazioni sulle modalità di visualizzazione in Gestione Report, vedere [pagina contenuto &#40;gestione Report&#41;](../../2014/reporting-services/contents-page-report-manager.md).  
  
 **Applica**  
 Fare clic per salvare le modifiche.  
  
 **Elimina**  
 Fare clic per rimuovere il modello dal database del server di report. Eliminando un modello non si elimina l'origine dati condivisa dipendente che fornisce informazioni di connessione, né si eliminano i report che utilizzano il modello come origine dati. Dopo l'eliminazione del modello, tuttavia, non è più possibile eseguire i report che utilizzano tale modello.  
  
 **Sposta**  
 Fare clic per spostare un modello nella gerarchia di cartelle del server di report. Verrà visualizzata la pagina di spostamento degli elementi nella quale è possibile esplorare le cartelle per selezionare un nuovo percorso. Per altre informazioni, vedere [pagina spostamento elementi &#40;gestione Report&#41;](../../2014/reporting-services/move-items-page-report-manager.md).  
  
 **Salvare**  
 Fare clic per salvare una copia di sola lettura della definizione del modello. In base alle associazioni di file definite nel computer, il file verrà aperto in [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] o in un'altra applicazione. Nella maggior parte dei casi, il modello viene aperto come file XML.  
  
 La copia aperta è identica alla definizione del modello originale pubblicata inizialmente nel server di report. Le eventuali proprietà impostate nel modello dopo la pubblicazione, ad esempio le proprietà dell'origine dati, non sono incluse nel file aperto.  
  
 È possibile modificare la definizione del modello e salvarla come nuovo file in una cartella condivisa, quindi caricare la definizione del modello nel server di report come nuovo elemento. Le modifiche apportate alla definizione del modello mentre il file è aperto in [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] o in un'altra applicazione non vengono salvate direttamente nel server di report. Per pubblicare il modello modificato nel server di report, è necessario caricare il file.  
  
 Si noti che se si desidera aprire il modello di report in Progettazione modelli, è necessario salvare il modello come file con estensione smdl, quindi aggiungere il file smdl a un progetto in Progettazione modelli.  
  
 **Sostituisci**  
 Fare clic per sostituire la definizione del modello con una definizione diversa di un file smdl incluso nel file system. Se si aggiorna una definizione di un modello, al termine dell'aggiornamento è necessario reimpostare le impostazioni dell'origine dati condivisa.  
  
 **Rigenera modello**  
 Fare clic per rigenerare un modello predefinito che sostituisce la versione corrente. Questa opzione viene visualizzata dopo la generazione del modello. Il modello generato è basato sull'origine dati condivisa. Non è possibile personalizzare il modello prima di generarlo. Dopo la generazione è tuttavia possibile fare clic su **Modifica** per aprire la definizione del modello, salvarla nel file system, quindi aggiungerla a un progetto in Progettazione modelli. Dopo avere personalizzato il modello, è possibile caricarlo nel server di report come nuovo elemento oppure fare clic su **Aggiorna** in questa pagina per sostituire il modello generato con la versione modificata in Progettazione modelli.  
  
## <a name="see-also"></a>Vedere anche  
 [Associare un report o un modello a un'origine dati condivisa &#40;SSRS&#41;](report-data/bind-a-report-or-model-to-a-shared-data-source-ssrs.md)   
 [Guida sensibile al contesto del server di report in Management Studio](tools/report-server-in-management-studio-f1-help.md)  
  
  
