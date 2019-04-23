---
title: Pagina nuova sottoscrizione o modifica sottoscrizione (gestione Report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: e02d6529-ce67-4305-b7f0-433997e99c21
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 926223ad0a5a8cdb1a5ff7aacfb7fdd7f84a8c57
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59940257"
---
# <a name="new-subscription-or-edit-subscription-page-report-manager"></a>Pagina Nuova sottoscrizione o Modifica sottoscrizione (Gestione report)
  La pagina Nuova sottoscrizione o Modifica sottoscrizione consente di creare una nuova sottoscrizione o modificare una sottoscrizione esistente per un report. Le opzioni disponibili in questa pagina variano a seconda dell'assegnazione di ruolo associata all'utente. Gli utenti con autorizzazioni avanzate avranno a disposizione un maggior numero di opzioni.  
  
 Le sottoscrizioni sono supportate per i report che possono essere eseguiti in modo automatico. È fondamentale che il report utilizzi credenziali archiviate o non utilizzi credenziali. Per i report con parametri è necessario specificare un valore predefinito. È possibile che le sottoscrizioni vengano disattivate se si modificano le impostazioni di esecuzione del report o si rimuovono i valori predefiniti per i parametri. Per altre informazioni, vedere [Creare e gestire sottoscrizioni per server di report in modalità nativa](../../2014/reporting-services/create-manage-subscriptions-native-mode-report-servers.md).  
  
> [!NOTE]  
>  Questa funzionalità non è disponibile in ogni edizione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vedere [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="navigation"></a>Navigazione  
 Utilizzare la procedura riportata di seguito per navigare fino a questo percorso nell'interfaccia utente.  
  
### <a name="to-open-the-new-subscription-or-edit-subscription-page"></a>Per aprire la pagina Nuova sottoscrizione o Modifica sottoscrizione  
  
1.  Aprire Gestione report e individuare il report per il quale si desidera aggiungere una sottoscrizione.  
  
2.  Passare con il puntatore del mouse sul report, quindi fare clic sulla freccia a discesa.  
  
3.  Nel menu a discesa eseguire uno dei passaggi seguenti:  
  
    -   fare clic su **Gestisci**. Verrà visualizzata la pagina delle proprietà Generale per il report. Selezionare la scheda **Sottoscrizioni** . Nella barra degli strumenti fare clic su **Nuova sottoscrizione**o selezionare una sottoscrizione esistente e fare clic su **Modifica**.  
  
    -   Fare clic su **Sottoscrivi**. Viene visualizzata la pagina **Nuova sottoscrizione** per il report.  
  
## <a name="options"></a>Opzioni  
 **Recapito**  
 Consente di selezionare l'estensione per il recapito da utilizzare per la distribuzione del report. In base all'estensione per il recapito selezionata, verranno visualizzate le impostazioni seguenti:  
  
-   Per le sottoscrizioni con recapito tramite posta elettronica sono disponibili opzioni di uso comune per gli utenti della posta elettronica, ad esempio i campi **A**, **Oggetto**e **Priorità** . Selezionare **Includi report** per incorporare o allegare il report oppure **Includi collegamento** per includere un URL nel report. L'opzione **Formato di rendering** consente di selezionare il formato di presentazione per il report allegato o incorporato.  
  
-   Le sottoscrizioni con recapito tramite condivisione file includono campi che consentono di specificare un percorso di destinazione. È possibile recapitare qualsiasi report in una condivisione file. Tuttavia, per i report che supportano funzionalità interattive (inclusi i report matrice che supportano il drill-down in righe e colonne) viene eseguito il rendering come file statici. Non è possibile visualizzare righe e colonne di drill-down in un file statico. Il nome della condivisione file deve essere specificato in formato Uniform Naming Convention (UNC) (ad esempio, \\\mycomputer\public\myreportfiles). Non includere una barra rovesciata finale nel nome del percorso. Il report verrà recapitato in un formato di file basato sul formato di rendering. Ad esempio, se si seleziona **Excel**il report viene recapitato come file con estensione xls.  
  
 Un'estensione per il recapito è disponibile se è installata e configurata nel server di report. Messaggio di posta elettronica da Server report è l'estensione per il recapito predefinita. Per poterla utilizzare, è tuttavia necessario configurarla. Il recapito alla condivisione file non richiede alcuna configurazione. Per poterlo utilizzare, è tuttavia è necessario definire una cartella condivisa.  
  
## <a name="subscription-processing-options"></a>Opzioni di elaborazione sottoscrizione  
 Utilizzare queste opzioni per impostare le condizioni per l'elaborazione della sottoscrizione. Alcune opzioni sono disponibili solo per i report con parametri o eseguiti come snapshot dell'esecuzione del report.  
  
 **Quando viene aggiornato il contenuto del report**  
 Selezionare questa opzione per sottoscrivere uno snapshot del report che viene aggiornato in base a una pianificazione. Questa opzione è disponibile solo se si sottoscrive un report eseguito come snapshot dell'esecuzione del report. Il contenuto di uno snapshot dell'esecuzione del report viene in genere aggiornato in base a una pianificazione. Per i report eseguiti in questa modalità è possibile impostare l'elaborazione della sottoscrizione quando viene aggiornato lo snapshot.  
  
 **Quando viene completata l'esecuzione pianificata del report**  
 Consente di creare una pianificazione che determina quando la sottoscrizione verrà elaborata.  
  
 **In una pianificazione condivisa**  
 Consente di selezionare una pianificazione predefinita per l'elaborazione della sottoscrizione.  
  
 **Immettere i valori dei parametri**  
 Utilizzare questa opzione per la sottoscrizione di un report con parametri. Questa opzione è disponibile solo per i report con parametri. Quando si crea una sottoscrizione a un report con parametri è possibile specificare i valori dei parametri utilizzati per creare la versione del report recapitata tramite la sottoscrizione. Ad esempio, è possibile specificare un codice area per selezionare i dati di vendita di un'area specifica. Se non si specifica un valore verrà utilizzato il valore predefinito.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare un Server di Report per il recapito tramite posta elettronica &#40;Gestione configurazione SSRS&#41;](../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)   
 [Gestione report &#40;modalità nativa SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Create, Modify, and Delete Schedules](subscriptions/create-modify-and-delete-schedules.md)   
 [Guida sensibile al contesto di Gestione report](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
