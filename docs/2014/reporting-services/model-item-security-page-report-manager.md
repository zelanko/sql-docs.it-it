---
title: Pagina sicurezza elemento modello (Gestione report) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.modelproperties.modelitemsecurity.f1
ms.assetid: 8c5b29ae-1f17-41f2-ab59-97899b8fb4fc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f45169a2fdc8fdc4d56cb27a8bf6348a3c3c1a29
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108227"
---
# <a name="model-item-security-page-report-manager"></a>Pagina sicurezza elemento modello (Gestione report)
  Questa pagina consente di proteggere parti di un modello concedendo o revocando autorizzazioni di sola lettura per elementi specifici. La sicurezza degli elementi dei modelli influisce sull'esplorazione ad hoc dei dati in fase di esecuzione e sulla possibilità di utilizzare parti di un modello pubblicato per la creazione di report in Generatore report. Per utilizzare questa caratteristica, è necessario disporre delle autorizzazioni Gestione contenuto.  
  
 La sicurezza degli elementi dei modelli si applica a un modello elaborato nel server di report e non influisce sui file con estensione smdl modificati in Progettazione modelli o utilizzati in Progettazione report. La sicurezza degli elementi dei modelli, inoltre, non ha effetto sugli utenti che dispongono dell'autorizzazione necessaria per modificare una definizione del modello. Qualsiasi utente che dispone di autorizzazioni Gestione contenuto o Pubblicazione in un modello può visualizzarne tutte le parti, indipendentemente dall'applicazione o meno della sicurezza degli elementi dei modelli.  
  
> [!NOTE]  
>  Gli elementi dei modelli possono essere protetti ulteriormente tramite l'utilizzo di filtri di sicurezza.  
  
 È possibile definire la sicurezza degli elementi dei modelli in entità, cartelle e singoli campi all'interno di un modello. Poiché un modello include una vasta gamma di elementi a cui è possibile applicare la sicurezza, l'ereditarietà delle autorizzazioni è integrata nel modello, in modo che sia possibile proteggere un numero elevato di elementi tramite un numero relativamente ridotto di assegnazioni di ruolo. L'ereditarietà delle autorizzazioni è basata sugli elementi seguenti:  
  
-   Modello  
  
-   Nodo radice  
  
-   Cartelle o entità  
  
-   Campi  
  
 Inizialmente, l'autorizzazione di accesso agli elementi del modello viene ereditata tramite le assegnazioni di ruolo impostate nel modello stesso. Un utente che dispone dell'autorizzazione per visualizzare un modello in una cartella in Gestione report può visualizzare tutti gli elementi del modello.  
  
 Se si applica la sicurezza degli elementi dei modelli, è necessario creare almeno un'assegnazione di ruolo nel nodo radice. Questa assegnazione di ruolo iniziale nel nodo radice diventa la nuova origine di autorizzazioni ereditate. L'assegnazione di ruolo nel nodo radice viene ereditata automaticamente da tutti gli elementi nella gerarchia del modello.  
  
 Per personalizzare ulteriormente le autorizzazioni per l'esplorazione dei dati, è possibile impostare autorizzazioni diverse in cartelle ed entità. È infine possibile impostare autorizzazioni nei singoli campi.  
  
 Per semplificare la gestione delle assegnazioni di ruolo, impostare le autorizzazioni solo nelle cartelle o nelle entità anziché in singoli campi. Non è possibile cercare le assegnazioni di ruolo create. Se si imposta la sicurezza in campi specifici e successivamente si desidera aggiornarne le impostazioni, è necessario esplorare lo spazio dei nomi del modello per individuare i campi per i quali è stata configurata la sicurezza.  
  
 Iniziare creando un'assegnazione di ruolo nel nodo radice, quindi creare assegnazioni di ruolo aggiuntive in entità e cartelle. Per annullare la sicurezza degli elementi del modello, deselezionare la casella di controllo **sicurezza indipendente dei singoli elementi del modello**. Se si deseleziona questa casella di controllo, vengono ripristinate le autorizzazioni iniziali ereditate dal modello.  
  
## <a name="navigation"></a>Navigazione  
 Utilizzare la procedura riportata di seguito per navigare fino a questo percorso nell'interfaccia utente.  
  
###### <a name="to-open-the-general-properties-page-for-a-report"></a>Per aprire la pagina delle proprietà Generale per un report  
  
1.  Aprire Gestione report, quindi individuare il modello per il quale si desidera configurare la sicurezza per gli elementi del modello.  
  
2.  Passare con il puntatore del mouse sul modello, quindi fare clic sulla freccia a discesa.  
  
3.  Scegliere **Gestisci**dal menu a discesa. Verrà visualizzata la pagina delle proprietà Generale per il modello.  
  
4.  Selezionare la scheda **Sicurezza elemento modello** .  
  
## <a name="options"></a>Opzioni  
 **sicurezza indipendente dei singoli elementi del modello**  
 Selezionare questa casella di controllo per attivare la sicurezza a livello di elemento del modello.  
  
 **Specificare le impostazioni di sicurezza per singoli elementi del modello**  
 Visualizza tutti gli elementi inclusi in un modello. È possibile spostarsi nello spazio dei nomi del modello per selezionare l'elemento per il quale si desidera impostare la sicurezza. È possibile selezionare un solo elemento per volta. Assicurarsi di creare la prima assegnazione di ruolo nel nodo radice prima di passare alle altre entità e cartelle.  
  
 **Eredita autorizzazioni dall'elemento padre**  
 Selezionare questa opzione per ereditare le impostazioni di sicurezza dell'elemento padre.  
  
 **Assegna autorizzazione di lettura ai seguenti utenti e gruppi (separati da un punto e virgola)**  
 Selezionare questa opzione per impostare l'account utente o di gruppo per il quale viene stabilito l'accesso. Se si utilizza la sicurezza predefinita, gli account utente o di gruppo corrispondono agli account di dominio di Windows. Specificare gli account nel formato: * \<dominio>\\<account\>*.  
  
## <a name="see-also"></a>Vedi anche  
 [Guida sensibile al contesto del server di report in Management Studio](tools/report-server-in-management-studio-f1-help.md)  
  
  
