---
title: Creare o personalizzare una libreria di Feed di dati (PowerPivot per SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data feed library
- data feeds [Analysis Services with SharePoint]
ms.assetid: 699fbeb9-42ab-436b-beba-214db51ea3dd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3586379cbd22dee4e288a032a9dd850355b2b674
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62749549"
---
# <a name="create-or-customize-a-data-feed-library-powerpivot-for-sharepoint"></a>Creare o personalizzare una libreria di feed di dati (PowerPivot per SharePoint)
  Una *libreria feed di dati* è una raccolta di SharePoint speciale che consente di registrare e condividere documenti di servizio dati Atom (atomsvc). Questi documenti forniscono feed di dati XML alle cartelle di lavoro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] o ad altre applicazioni client che supportano il formato di feed di dati Atom. Una libreria di feed di dati è diversa dalle altre raccolte di SharePoint poiché consente di:  
  
-   Creare o modificare un *documento di servizio dati*usato per specificare una connessione HTTP a un feed specifico.  
  
-   Condividere e gestire documenti di servizio dati in un percorso principale.  
  
-   Identificare visivamente i documenti di servizio dati tramite un'icona, in modo che sia possibile distinguere facilmente i documenti di servizio da altri documenti archiviati nella stessa raccolta: ![GMNI_IconDataFeed](../media/gmni-icondatafeed.gif "GMNI_IconDataFeed")  
  
 In una libreria di feed di dati sono sempre contenuti i file del documento di servizio dati (con estensione atomsvc) e mai il feed di dati stesso. A differenza di un feed di dati che è costituito da dati XML statici, il documento di servizio dati consente di specificare un URL a un servizio o un'applicazione che permette di generare un feed durante la richiesta, fornendo informazioni di connessione riutilizzabili per operazioni di importazione ripetibili.  
  
 In questo argomento sono incluse le sezioni seguenti:  
  
 [Prerequisiti](#prereq)  
  
 [Creare una nuova libreria di feed di dati](#createlib)  
  
 [Aggiungere il tipo di contenuto del feed di dati a qualsiasi libreria](#addtolib)  
  
##  <a name="prereq"></a> Prerequisiti  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] L'integrazione della funzionalità PowerPivot deve essere attiva per i siti per cui si intende creare la libreria di feed di dati. Se il tipo di modello di libreria di feed di dati non è disponibile, la causa più probabile è il mancato rispetto di questo prerequisito. Per altre informazioni, vedere [attivare integrazione della caratteristica PowerPivot per le raccolte siti in Amministrazione centrale](activate-power-pivot-integration-for-site-collections-in-ca.md).  
  
 Per creare la libreria è necessario essere proprietari del sito.  
  
##  <a name="createlib"></a> Creare una nuova libreria di feed di dati  
 La creazione di una libreria di feed di dati è il primo passaggio per abilitare i feed di dati per le cartelle di lavoro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Poiché tramite una libreria di feed di dati vengono fornite pagine dell'applicazione e di gestione per i documenti di servizio dati, è necessario disporre di questa libreria prima di creare un nuovo documento.  
  
 Una libreria di feed di dati si basa su un modello predefinito e su un *tipo di contenuto del documento di servizio dati* preconfigurato che consente di definire le proprietà e i comportamenti per un documento di servizio dati.  
  
1.  Scegliere **Azioni sito** nell'angolo superiore sinistro della pagina.  
  
2.  Fare clic su **altre opzioni**...  
  
3.  In Librerie scegliere **Libreria feed di dati**.  
  
4.  Digitare le preferenze di versione, avvio, descrizione e nome. Includere informazioni descrittive per assistere gli utenti nell'identificazione di questa libreria come archiviazione per i documenti di servizio dati.  
  
5.  Fare clic su **Crea**.  
  
 Verrà visualizzato un collegamento alla libreria di feed di dati nel riquadro di navigazione Avvio Veloce per il sito corrente.  
  
 Dopo avere creato una libreria, è possibile utilizzarla per creare documenti di servizio dati. Per altre informazioni, vedere [usare feed di dati &#40;PowerPivot per SharePoint&#41;](use-data-feeds-power-pivot-for-sharepoint.md).  
  
##  <a name="addtolib"></a> Aggiungere il tipo di contenuto del feed di dati a qualsiasi libreria  
 Se non si desidera creare una libreria di feed di dati dedicata, ma si desidera creare e gestire documenti di servizio dati da un sito di SharePoint, è possibile aggiungere e configurare manualmente il tipo di contenuto del documento di servizio dati per qualsiasi libreria che si utilizzerà per condividere i file del documento di servizio dati (con estensione atomsvc).  
  
 È necessario disporre almeno dell'autorizzazione Gestione elenchi per aggiungere e configurare un tipo di contenuto. Questa autorizzazione viene compilata nel livello di autorizzazione Progettazione e superiore.  
  
 I passaggi seguenti devono essere ripetuti per ogni libreria in cui si desidera creare o modificare i documenti di registrazione del feed di dati.  
  
#### <a name="step-1-enable-content-type-management"></a>Passaggio 1: Abilitare la gestione dei tipi di contenuto  
  
1.  Aprire la raccolta documenti per cui si desidera abilitare più tipi di contenuto.  
  
2.  Sulla barra multifunzione di SharePoint, in Strumenti raccolta fare clic su **Raccolta**.  
  
3.  Fare clic su **Impostazioni**.  
  
4.  Fare clic su **Impostazioni raccolta**.  
  
5.  In Impostazioni generali scegliere **Impostazioni avanzate**.  
  
6.  In Tipi di contenuto nella sezione "Consenti la gestione di più tipi di contenuto:" scegliere **Sì**.  
  
7.  Fare clic su **OK**.  
  
#### <a name="step-2-add-the-data-service-document-content-type"></a>Passaggio 2: Aggiungere il tipo di contenuto documento di servizio dati  
  
1.  Nella sezione Tipi di contenuto fare clic su **Aggiungi da tipi di contenuto del sito esistenti**. Se questa pagina non viene visualizzata, tornare al sito, fare clic su **Raccolta** in Strumenti raccolta, quindi scegliere **Impostazioni raccolta**.  
  
2.  In Tipi di contenuto fare clic su **Aggiungi da tipi di contenuto del sito esistenti**.  
  
3.  In Seleziona tipi di contenuto del sito da: scegliere **Business Intelligence**.  
  
4.  In Tipi di contenuto del sito disponibili scegliere **Documento di servizio dati**, quindi fare clic su **Aggiungi** per spostare il tipo di contenuto selezionato nell'elenco Tipi di contenuto da aggiungere.  
  
5.  Fare clic su **OK**.  
  
#### <a name="step-3-verify-data-service-document-configuration"></a>Passaggio 3: Verifica della configurazione di documento di servizio dati  
  
1.  Aprire la home page del sito.  
  
2.  Aprire la raccolta.  
  
3.  Sulla barra multifunzione di SharePoint fare clic su **Documenti**.  
  
4.  Fare clic sulla freccia GIÙ su Nuovo documento e selezionare **Documento di servizio dati**. Verrà visualizzata la pagina Nuovo documento di servizio dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Usare feed di dati &#40;PowerPivot per SharePoint&#41;](use-data-feeds-power-pivot-for-sharepoint.md)   
 [Eliminare una libreria di Feed di dati PowerPivot](delete-a-power-pivot-data-feed-library.md)   
 [Amministrazione Server PowerPivot e la configurazione in Amministrazione centrale](power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [Feed di dati PowerPivot](power-pivot-data-feeds.md)  
  
  
