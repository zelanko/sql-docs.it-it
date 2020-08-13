---
title: Uso di sottoscrizioni (portale Web) | Microsoft Docs
description: Informazioni su come usare la pagina Sottoscrizioni per visualizzare un elenco di tutte le sottoscrizioni del report corrente in Reporting Services.
ms.date: 01/31/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 09e8ece5-0200-41f2-87c1-9fab19e261be
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d5d936933b96c8d7f5c4c2830707b4a6bb4d9fe2
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243553"
---
# <a name="working-with-subscriptions-web-portal"></a>Uso di sottoscrizioni (portale Web)

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

L'uso della pagina Sottoscrizioni consente di visualizzare un elenco di tutte le sottoscrizioni del report corrente. Se sono disponibili autorizzazioni sufficienti (quelle assegnate dall'attività Gestione di tutte le sottoscrizioni) è possibile visualizzare le sottoscrizioni di tutti gli utenti. In caso contrario, in questa pagina vengono visualizzate solo le sottoscrizioni personali.  
  
Prima di creare una nuova sottoscrizione, è necessario verificare che l'origine dati del report utilizzi credenziali archiviate. Per archiviare le credenziali, utilizzare la pagina delle proprietà Origini dati.  
  
> [!NOTE]
> È necessario avviare il servizio SQL Server Agent.   
  
![Gestire le sottoscrizioni](../reporting-services/media/working-with-subscriptions-web-portal/ssrs-manage-subscriptions.png)  
Per passare alla pagina Sottoscrizioni, fare clic sul pulsante con i puntini di sospensione **(...)** di un report, selezionare **Gestisci** e quindi **Sottoscrizioni**.  
  
Nella pagina sottoscrizioni è possibile creare nuove sottoscrizioni selezionando **+ Nuova sottoscrizione**. È possibile modificare le sottoscrizioni esistenti o eliminare quelle selezionate.  
  
Questa pagina include anche lo stato dei risultati delle esecuzioni della sottoscrizione nella colonna **Risultato** . Se si è verificato un errore per una sottoscrizione, è consigliabile controllare prima la colonna dei risultati per visualizzare il contenuto del messaggio. 

È anche possibile eseguire una sottoscrizione quando si desidera selezionando **Esegui ora** nella pagina Sottoscrizioni.
  
## <a name="creating-or-editing-a-subscription"></a>Creazione o modifica di una sottoscrizione  
La pagina Nuova sottoscrizione o Modifica sottoscrizione consente di creare una nuova sottoscrizione o modificare una sottoscrizione esistente per un report. Le opzioni disponibili in questa pagina variano a seconda dell'assegnazione di ruolo associata all'utente. Gli utenti con autorizzazioni avanzate avranno a disposizione un maggior numero di opzioni.  
  
Le sottoscrizioni sono supportate per i report che possono essere eseguiti in modo automatico. È fondamentale che il report utilizzi credenziali archiviate o non utilizzi credenziali. Per i report con parametri è necessario specificare un valore predefinito. È possibile che le sottoscrizioni vengano disattivate se si modificano le impostazioni di esecuzione del report o si rimuovono i valori predefiniti per i parametri. Per altre informazioni, vedere [Creare e gestire sottoscrizioni per server di report in modalità nativa](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md).  
  
## <a name="type-of-subscription"></a>Tipo di sottoscrizione  
È possibile selezionare una **sottoscrizione standard** o una **sottoscrizione guidata dai dati**.  
  
![ssRSWebPortal-subscriptions3](../reporting-services/media/working-with-subscriptions-web-portal/ssrswebportal-subscriptions3.png)  
   
Una sottoscrizione guidata dai dati esegue una query su un database sottoscrittore per ottenere informazioni sulla sottoscrizione ogni volta che la sottoscrizione viene eseguita. Le sottoscrizioni guidate dai dati utilizzano i risultati della query per determinare i destinatari della sottoscrizione, le impostazioni di recapito e i valori dei parametri del report. In fase di esecuzione, il server di report esegue una query per recuperare i valori utilizzati per le impostazioni di sottoscrizione.   
  
Per creare una sottoscrizione guidata dai dati è necessario sapere come scrivere una query o un comando per il recupero dei dati per la sottoscrizione. È anche necessario disporre di un archivio dati contenente i dati del sottoscrittore, ad esempio, nomi e indirizzi di posta elettronica, da usare per la sottoscrizione.  
  
Questa opzione è disponibile per gli utenti con autorizzazioni avanzate. Se si utilizzano le impostazioni di sicurezza predefinite, le sottoscrizioni guidate dai dati non possono essere utilizzate per i report inclusi nelle cartelle Report personali.  
  
## <a name="destination"></a>Destination  
Consente di selezionare l'estensione per il recapito da utilizzare per la distribuzione del report.   
  
Un'estensione per il recapito è disponibile se è installata e configurata nel server di report. Posta elettronica del server report è l'estensione per il recapito predefinita. Per poterla usare, è tuttavia necessario configurarla. Il recapito alla condivisione file non richiede alcuna configurazione. Per poterlo utilizzare, è tuttavia è necessario definire una cartella condivisa.  
  
![ssRSWebPortal-subscriptions2](../reporting-services/media/working-with-subscriptions-web-portal/ssrswebportal-subscriptions2.png)  
  
In base all'estensione per il recapito selezionata, verranno visualizzate le impostazioni seguenti:  
  
-   Per le sottoscrizioni con recapito tramite posta elettronica sono disponibili opzioni di uso comune per gli utenti della posta elettronica, ad esempio i campi A, Oggetto e Priorità. Selezionare **Includi report** per incorporare o allegare il report oppure **Includi collegamento** per includere un URL nel report. L'opzione **Formato di rendering** consente di selezionare il formato di presentazione per il report allegato o incorporato. Per informazioni dettagliate, vedere [Creare una sottoscrizione con recapito tramite posta elettronica](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md#bkmk_create_email_subscription). 
  
-   Le sottoscrizioni con recapito tramite condivisione file includono campi che consentono di specificare un percorso di destinazione. È possibile recapitare qualsiasi report in una condivisione file. Tuttavia, per i report che supportano funzionalità interattive (inclusi i report matrice che supportano il drill-down in righe e colonne) viene eseguito il rendering come file statici. Non è possibile visualizzare righe e colonne di drill-down in un file statico. Il nome della condivisione file deve essere specificato in formato UNC (Uniform Naming Convention), ad esempio \mycomputer\public\myreportfiles. Non includere una barra rovesciata finale nel nome del percorso. Il report verrà recapitato in un formato di file basato sul formato di rendering. Ad esempio, se si seleziona Excel, il report viene recapitato come file con estensione xlsx.  Per informazioni dettagliate, vedere [Creare una sottoscrizione con recapito tramite condivisione file](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md#bkmk_create_fileshare_subscription).
  
## <a name="data-driven-subscription-dataset"></a>Set di dati della sottoscrizione guidata dai dati  
Per una sottoscrizione guidata dai dati, è necessario definire il set di dati usato per la sottoscrizione. Selezionare **Modifica set di dati** per specificare tali informazioni.  
  
![ssRSWebPortal-subscriptions4](../reporting-services/media/working-with-subscriptions-web-portal/ssrswebportal-subscriptions4.png)  
  
È necessario innanzitutto specificare un' **origine dati** da usare per la query. Può essere un'origine dati condivisa oppure è possibile specificare un'origine dati personalizzata.  
  
Sarà quindi necessario fornire una **query** in cui verranno elencate le diverse opzioni necessarie per l'esecuzione della sottoscrizione. Nella schermata verranno visualizzati i campi che devono essere restituiti. Questi campi possono variare a seconda del metodo di recapito e dei parametri del report.  
  
Per ottenere risultati migliori, eseguire la query in SQL Server Management Studio prima di utilizzarla nella sottoscrizione guidata dai dati. È quindi possibile analizzare i risultati per verificare che contengano le informazioni necessarie. Gli aspetti importanti da tenere presenti nei risultati della query sono i seguenti:  
  
-   Le colonne nel set di risultati determinano i valori che è possibile specificare per le opzioni di recapito e i parametri del report. Ad esempio, se si sta creando una sottoscrizione guidata dai dati per il recapito tramite posta elettronica, è necessario avere una colonna di indirizzi di posta elettronica.  
  
-   Le righe nel set di risultati determinano il numero di recapiti del report generati. Se sono presenti 10.000 righe, il server di report genererà 10.000 notifiche e recapiti.  
  
![ssRSWebPortal-subscriptions5](../reporting-services/media/working-with-subscriptions-web-portal/ssrswebportal-subscriptions5.png)  
  
È quindi possibile convalidare la query. È inoltre possibile definire un **timeout per la query**.  
  
Al termine della creazione della query, è possibile assegnare valori ai campi obbligatori. È possibile immettere i dati manualmente o selezionare un campo dal set di dati creato. 

## <a name="next-steps"></a>Passaggi successivi

[Creare e gestire sottoscrizioni per server di report in modalità nativa](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)
[Portale Web](../reporting-services/web-portal-ssrs-native-mode.md)  
[Uso di report impaginati (portale Web)](working-with-paginated-reports-web-portal.md)  
[Usare i set di dati condivisi (portale Web)](../reporting-services/work-with-shared-datasets-web-portal.md)

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
