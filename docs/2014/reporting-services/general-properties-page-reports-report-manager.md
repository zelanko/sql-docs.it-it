---
title: Pagina delle proprietà generale, report (Gestione report) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 66c99d28-ab41-45f0-bf02-ed560293595d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3b89d67636dd28514b8d5f34bee423e60abd9b81
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109099"
---
# <a name="general-properties-page-reports-report-manager"></a>Pagina delle proprietà Generale, Report (Gestione report)
  La pagina delle proprietà Generale per i report consente di rinominare, eliminare, spostare o sostituire la definizione del report. È inoltre possibile utilizzare questa pagina per creare un report collegato. Nella parte superiore della pagina vengono visualizzati il nome dell'utente che ha creato o modificato il report e la data e ora di modifica.  
  
## <a name="navigation"></a>Navigazione  
 Utilizzare la procedura riportata di seguito per navigare fino a questo percorso nell'interfaccia utente.  
  
###### <a name="to-open-the-general-properties-page-for-a-report"></a>Per aprire la pagina delle proprietà Generale per un report  
  
1.  Aprire Gestione report, quindi individuare il report per il quale si desidera visualizzare o configurare le proprietà.  
  
2.  Passare con il puntatore del mouse sul report, quindi fare clic sulla freccia a discesa.  
  
3.  Scegliere **Gestisci**dal menu a discesa. Verrà visualizzata la pagina delle proprietà Generale per il report.  
  
## <a name="options"></a>Opzioni  
 **Nome**  
 Digitare un nome per il report. Il nome deve includere almeno un carattere alfanumerico. È inoltre possibile utilizzare spazi e alcuni simboli. Non utilizzare i caratteri ; ? : \@ & = +, $ *\< >  
  
 " o / quando si specifica un nome.  
  
 **Descrizione**  
 Consente di digitare una descrizione del report. Questa descrizione viene visualizzata nella pagina Contenuto per gli utenti autorizzati ad accedere al report.  
  
 **Nascondi in visualizzazione Elenco**  
 Selezionare questa opzione per fare in modo che il report non venga visualizzato per gli utenti che utilizzano la modalità di visualizzazione Elenco in Gestione report. La modalità di visualizzazione Elenco è il formato di visualizzazione predefinito utilizzato per l'esplorazione della gerarchia di cartelle del server di report. Nella visualizzazione Elenco i nomi e le descrizioni degli elementi vengono disposti dall'alto in basso nella pagina. Il formato alternativo è costituito dalla visualizzazione Dettagli, in cui non sono incluse le descrizioni ma sono disponibili altre informazioni sugli elementi. Gli elementi possono essere nascosti nella visualizzazione Elenco ma non nella visualizzazione Dettagli. Se si desidera limitare l'accesso a un elemento, è necessario creare un'assegnazione di ruolo.  
  
 **Applica**  
 Fare clic per salvare le modifiche.  
  
 **Elimina**  
 Fare clic per rimuovere il report dal database del server di report. L'eliminazione di un report determina l'eliminazione dell'intera cronologia del report e di tutte le pianificazioni e sottoscrizioni associate specifiche del report. Se il report è associato a report collegati, i report collegati vengono invalidati.  
  
 **Spostamento**  
 Fare clic per spostare un report nella gerarchia di cartelle del server di report. Verrà visualizzata la pagina di spostamento degli elementi nella quale è possibile esplorare le cartelle per selezionare un nuovo percorso. Per ulteriori informazioni, vedere la [pagina di spostamento degli elementi &#40;Gestione report&#41;](../../2014/reporting-services/move-items-page-report-manager.md).  
  
 **Crea report collegato**  
 Fare clic per aprire la pagina Nuovo report collegato. Per ulteriori informazioni su questa pagina e sui report collegati, vedere la [pagina nuovo report collegato &#40;Gestione report&#41;](../../2014/reporting-services/new-linked-report-page-report-manager.md).  
  
 **Salva**  
 Fare clic per estrarre una copia di sola lettura della definizione del report. In base alle associazioni di file definite nel computer, il file verrà aperto in [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] o in un'altra applicazione. Nella maggior parte dei casi, il report viene aperto come file XML.  
  
 La copia che viene aperta è identica alla definizione del report originale pubblicata inizialmente nel server di report. Le eventuali proprietà impostate nel report dopo la pubblicazione (ad esempio, parametri e proprietà dell'origine dei dati) non sono disponibili nel file della definizione aperto.  
  
 È possibile modificare la definizione del report e salvarla come un nuovo file in una cartella condivisa, quindi caricare la definizione del report come un nuovo elemento nel server di report. Le modifiche apportate alla definizione del report mentre il file è aperto in [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] o in un'altra applicazione non vengono salvate direttamente nel server di report. Per pubblicare il report modificato nel server di report è necessario caricare il file.  
  
 **Sostituire**  
 Fare clic per sostituire la definizione del report utilizzata nel report corrente con una definizione diversa contenuta in un file con estensione rdl presente nel file system. Se si aggiorna la definizione di un report è necessario reimpostare le impostazioni dell'origine dei dati dopo l'aggiornamento.  
  
 **Modifica collegamento**  
 Fare clic per selezionare una definizione del report diversa per il report collegato. Questa opzione viene visualizzata se si tratta di un report collegato. In questo caso, è possibile impostare questa proprietà per sostituire la definizione del report.  
  
## <a name="see-also"></a>Vedi anche  
 [Gestione report &#40;modalità nativa SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Guida sensibile al contesto di Gestione report](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
