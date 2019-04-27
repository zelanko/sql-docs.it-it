---
title: Creare una connessione BI Semantic Model a una cartella di lavoro di PowerPivot | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: b2e3f97f-18a8-42b6-9030-b4f818afc3b9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4ad60799fa8590609cabd2e1e1fdfd8d7493c282
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62749573"
---
# <a name="create-a-bi-semantic-model-connection-to-a-powerpivot-workbook"></a>Creare una connessione BISM (BI Semantic Model) a una cartella di lavoro di PowerPivot
  Utilizzare le informazioni di questo argomento per impostare una connessione BISM che reindirizza a una cartella di lavoro di PowerPivot nella stessa farm.  
  
 Dopo avere creato una connessione BISM e configurato le autorizzazioni di SharePoint, sarà possibile utilizzare la connessione come origine dati per i report di Excel o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] .  
  
 In questo argomento sono incluse le sezioni seguenti. Eseguire ogni attività nell'ordine indicato.  
  
 [Verificare i prerequisiti](#bkmk_prereq)  
  
 [Creare una connessione](#bkmk_create)  
  
 [Configurare autorizzazioni di SharePoint sulla connessione BISM](#bkmk_permissions)  
  
 [Configurare autorizzazioni di SharePoint sulla cartella di lavoro](#bkmk_userdb)  
  
 [Passaggi successivi](#bkmk_next)  
  
##  <a name="bkmk_prereq"></a> Verificare i prerequisiti  
 Per creare un file di connessione BISM, è necessario disporre delle autorizzazioni di collaborazione.  
  
 È necessario disporre di una raccolta che supporta il tipo di contenuto della connessione BISM. Per altre informazioni, vedere [aggiungere una BI Semantic Model tipo di contenuto connessione a una raccolta &#40;PowerPivot per SharePoint&#41;](add-bi-semantic-model-connection-content-type-to-library.md).  
  
 È necessario conoscere l'URL della cartella di lavoro di PowerPivot per cui si imposta una connessione BI semantic model (ad esempio, http://adventure-works/shared myworkbook). La cartella di lavoro deve essere nella stessa farm.  
  
 Tutti i computer e gli utenti che partecipano nella sequenza di connessione devono essere nello stesso dominio o nel dominio attendibile (attendibilità bidirezionale).  
  
##  <a name="bkmk_create"></a> Creare una connessione  
  
1.  Nella raccolta che conterrà la connessione BISM, fare clic su **Documenti** sulla barra multifunzione di SharePoint. Fare clic sulla freccia GIÙ su Nuovo documento e selezionare **File di connessione BISM** per aprire la pagina Nuova connessione BISM.  
  
     ![Sottomenu nuovo documento in una raccolta di SharePoint](../media/ssas-bismconnection-new.gif "sottomenu nuovo documento in una raccolta di SharePoint")  
  
2.  Impostare il **Server** proprietà all'URL di SharePoint della cartella di lavoro di PowerPivot (ad esempio  **http://mysharepoint/shared myworkbook**. In una distribuzione di PowerPivot per SharePoint i dati possono essere caricati in qualsiasi server nella farm. Per questo motivo, le connessioni alle origine dati ai dati PowerPivot consentono di specificare solo il percorso alla cartella di lavoro. Il servizio di sistema PowerPivot consente di determinare il server tramite cui vengono caricati i dati.  
  
     Non usare la **Database** proprietà; non viene usato quando si specifica il percorso di una cartella di lavoro di PowerPivot.  
  
     La pagina dovrebbe essere simile a quanto illustrato nella figura seguente.  
  
     ![Pagina di connessione BISM con URL alla cartella di lavoro](../media/ssas-bismconnection-ppvtds.gif "pagina della connessione BISM che mostra URL alla cartella di lavoro")  
  
     Facoltativamente, se si dispone di autorizzazioni di SharePoint per la cartella di lavoro, viene eseguito un passaggio di convalida aggiuntivo, per verificare la validità del percorso. Se non si dispone dell'autorizzazione per accedere ai dati, è possibile salvare la connessione BISM senza la risposta della convalida.  
  
##  <a name="bkmk_permissions"></a> Configurare autorizzazioni di SharePoint sulla connessione BISM  
 Per utilizzare una connessione BISM come origine dati per una cartella di lavoro di Excel o un report di Reporting Services, sono necessarie autorizzazioni **Lettura** sull'elemento della connessione BISM in una raccolta di SharePoint. Nel livello di autorizzazione di lettura è inclusa l'autorizzazione **Apertura elementi** che consente di scaricare le informazioni sulla connessione BISM in un'applicazione desktop di Excel.  
  
 Sono disponibili diversi modi per concedere le autorizzazioni in SharePoint. Le istruzioni seguenti illustrano come creare un nuovo gruppo denominato **Utenti BISM** con il livello di autorizzazione di **lettura** .  
  
 Per modificare le autorizzazioni è necessario essere proprietari del sito.  
  
1.  In Azioni sito fare clic su **Autorizzazioni sito**.  
  
2.  Fare clic su **Crea gruppo** e assegnare al nuovo gruppo il nome **Utenti BISM**.  
  
3.  Scegliere il livello di autorizzazione **Lettura** e fare clic su **Crea**.  
  
4.  Selezionare **Utenti BISM** in Utenti e gruppi.  
  
5.  Scegliere Nuovo, fare clic su **Aggiungi utenti**, quindi aggiungere account utente o di gruppo.  
  
     Questi utenti e gruppi disporranno di autorizzazioni di lettura per tutto il sito, incluse tutte le raccolte e gli elenchi che ereditano le autorizzazioni dal livello del sito. Se tali autorizzazioni sono troppo elevate, è possibile rimuovere selettivamente il gruppo da raccolte, elenchi o elementi specifici.  
  
 Per rimuovere selettivamente le autorizzazioni al livello dell'elemento, effettuare le operazioni seguenti:  
  
1.  In una raccolta, selezionare un documento. Fare clic sulla freccia GIÙ a destra e scegliere **Gestisci autorizzazioni**.  
  
2.  Per impostazione predefinita, un elemento eredita le autorizzazioni. Per modificare le autorizzazioni di singoli documenti in questa raccolta, fare clic su **Interrompi ereditarietà autorizzazioni**.  
  
3.  Selezionare la casella di controllo accanto a **Utenti BISM**.  
  
4.  Fare clic su **Rimuovi autorizzazioni utente**.  
  
##  <a name="bkmk_userdb"></a> Configurare autorizzazioni di SharePoint sulla cartella di lavoro  
 Se si utilizza un database PowerPivot in una cartella di lavoro di Excel, le autorizzazioni di SharePoint per la cartella di lavoro di Excel determinano l'accesso ai dati tramite la connessione BISM. Tutti gli utenti che accedono alla cartella di lavoro devono disporre delle autorizzazioni di lettura sulla cartella di lavoro per poterla utilizzare come origine dati esterna.  
  
 Se è stato creato un gruppo **Utenti BISM** con le istruzioni della sezione precedente, gli account utente e di gruppo che sono membri del gruppo **Utenti BISM** hanno autorizzazioni sufficienti sulla cartella di lavoro e sul file di connessione BI Semantic Model, presupponendo che la cartella di lavoro usi autorizzazioni ereditate.  
  
##  <a name="bkmk_next"></a> Passaggi successivi  
 Dopo avere creato e protetto una connessione BISM è possibile specificarla come origine dati. Per altre informazioni, vedere [Utilizzare una connessione BISM (BI Semantic Model) in Excel o Reporting Services](use-a-bi-semantic-model-connection-in-excel-or-reporting-services.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Connessione BI Semantic Model di PowerPivot &#40;con estensione bism&#41;](power-pivot-bi-semantic-model-connection-bism.md)   
 [Utilizzare una connessione BISM (BI Semantic Model) in Excel o Reporting Services](use-a-bi-semantic-model-connection-in-excel-or-reporting-services.md)   
 [Creare una connessione BISM a un database modello tabulare](create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)  
  
  
