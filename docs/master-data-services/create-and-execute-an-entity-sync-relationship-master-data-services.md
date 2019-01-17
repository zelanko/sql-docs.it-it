---
title: Creare ed eseguire una relazione di sincronizzazione delle entità (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 0ddceab4-d2b3-4bc1-bd9c-6b852200b414
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: ff4c4ae12021930ba447c3cb01a9830907fb3153
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52822915"
---
# <a name="create-and-execute-an-entity-sync-relationship-master-data-services"></a>Creare ed eseguire una relazione di sincronizzazione delle entità (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  La sincronizzazione delle entità è una sincronizzazione unidirezionale e ripetibile tra le versioni dell'entità. Consente di condividere i dati delle entità tra i vari modelli.  
  
## <a name="prerequisites"></a>Prerequisites  
 Prerequisiti per creare una relazione di sincronizzazione delle entità:  
  
-   È necessaria l'autorizzazione per accedere all'area funzionale Amministrazione sistema. Per altre informazioni, vedere [Autorizzazioni per aree funzionali &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   È necessario essere un amministratore del modello per il modello di destinazione. Per altre informazioni, vedere [Amministratori &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   È necessario avere almeno l'accesso in lettura all'entità di origine e a tutti i relativi attributi e membri.  
  
 Prerequisiti per eseguire una relazione di sincronizzazione delle entità:  
  
-   È necessaria l'autorizzazione per accedere all'area funzionale Amministrazione sistema. Per altre informazioni, vedere [Autorizzazioni per aree funzionali &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   È necessario essere un amministratore del modello per il modello di destinazione. Per altre informazioni, vedere [Amministratori &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
 Quando si crea una relazione di sincronizzazione delle entità, tenere presente i fattori seguenti:  
  
-   Le entità di origine e di destinazione devono essere in modelli diversi.  
  
-   Non deve essere stato eseguito il commit di una versione dell'entità di destinazione.  
  
-   Dopo aver stabilito una relazione di sincronizzazione, la destinazione viene immediatamente sincronizzata con l'origine.  
  
-   Una versione dell'entità di destinazione non può essere una versione dell'entità di origine di un'altra relazione di sincronizzazione.  
  
 Quando si esegue una relazione di sincronizzazione delle entità, tenere presente i fattori seguenti:  
  
-   Verranno copiati solo i membri foglia.  
  
-   Gli attributi basati su dominio non verranno copiati.  
  
-   I membri temporaneamente eliminati non verranno copiati.  
  
-   La sincronizzazione non genera transazioni o cronologie dell'entità di destinazione.  
  
 **Per creare una relazione di sincronizzazione delle entità**  
  
1.  In Gestione dati master fare clic su **Amministrazione sistema**.  
  
2.  Nella pagina **Vista modelli** scegliere **Gestisci** dalla barra dei menu, quindi fare clic su **Entity Sync**(Sincronizzazione entità).  
  
3.  Nella pagina di **manutenzione della sincronizzazione delle entità** fare clic su **Aggiungi**. Viene visualizzato un riquadro sul lato destro.  
  
4.  Selezionare un modello dall'elenco **Modello** dell'origine.  
  
5.  Selezionare una versione dall'elenco **Versione** dell'origine.  
  
6.  Selezionare un'entità dall'elenco **Entità** dell'origine.  
  
7.  Selezionare un modello dall'elenco **Modello** della destinazione.  
  
8.  Selezionare una versione dall'elenco **Versione** della destinazione.  
  
9. Scegliere **Existing Entity** (Entità esistente) e selezionare un'entità dall'elenco per sincronizzare un'entità già esistente oppure scegliere **Nuova entità** e immettere il nome dell'entità di destinazione per eseguire la sincronizzazione con una nuova entità.  
  
10. Selezionare **Sincronizza su richiesta**oppure **Auto Sync** (Sincronizzazione automatica) e impostare una frequenza.  
  
11. Fare clic su **Salva**.  
  
 **Per eseguire una relazione di sincronizzazione delle entità**  
  
1.  In Gestione dati master fare clic su **Amministrazione sistema**.  
  
2.  Nella pagina **Vista modelli** scegliere **Gestisci** dalla barra dei menu, quindi fare clic su **Entity Sync**(Sincronizzazione entità).  
  
3.  Nella pagina di **gestione della sincronizzazione delle entità** selezionare una relazione di sincronizzazione nella griglia.  
  
4.  Fare clic su **Esegui**.  
  
## <a name="sync-relationship-information"></a>Informazioni sulle relazioni di sincronizzazione  
 Per ogni relazione di sincronizzazione creata, viene aggiunta alla griglia una riga con dieci colonne. La tabella seguente descrive le colonne.  
  
|colonna|Descrizione|  
|------------|-----------------|  
|Stato|Stato della relazione di sincronizzazione.<br /><br /> Quando si fa clic su **Salva** o si esegue una relazione di sincronizzazione, viene visualizzata l'immagine ![Icona di aggiornamento dello stato](../master-data-services/media/mds-statusicon-updating.png "Icona di aggiornamento dello stato") che indica che è in corso l'aggiornamento dell'attributo.<br /><br /> Se si verificano errori durante la creazione, la modifica o l'esecuzione di una relazione di sincronizzazione, viene visualizzata l'immagine ![Icona di errore](../master-data-services/media/mds-statusicon-error.png "Icona di errore").<br /><br /> In caso contrario lo stato è OK e viene visualizzata l'immagine ![Icona di stato OK](../master-data-services/media/mds-statusicon-ok.png "Icona di stato OK").|  
|Modello di origine|Nome del modello di origine.|  
|Versione di origine|Nome della versione di origine.|  
|Entità di origine|Nome dell'entità di origine.|  
|Modello di destinazione|Nome del modello di destinazione.|  
|Versione di destinazione|Nome della versione di destinazione.|  
|Entità di destinazione|Nome dell'entità di destinazione.|  
|Frequenza|Specifica la frequenza della relazione di sincronizzazione.|  
|Ora dell'ultimo tentativo|Indica l'ora in cui si è verificato l'ultimo tentativo di sincronizzazione.|  
|Ultimo tentativo riuscito|Indica l'ora in cui si è verificato l'ultimo tentativo di sincronizzazione riuscito.|  
  
 Quando si fa clic su un indice, vengono visualizzate le informazioni seguenti.  
  
-   **Last Attempt Error** (Errore ultimo tentativo): informazioni sugli errori dell'ultimo tentativo di sincronizzazione.  
  
-   **Creato da**: Nome dell'utente che ha creato la sincronizzazione.  
  
-   **Il**: data e ora di creazione della sincronizzazione.  
  
-   **Aggiornato da**: nome dell'utente che ha aggiornato la sincronizzazione per ultimo.  
  
-   **Il**: data e ora dell'ultimo aggiornamento della sincronizzazione.  
  
## <a name="next-steps"></a>Next Steps  
 [Modificare ed eliminare una relazione di sincronizzazione delle entità &#40;Master Data Services&#41;](../master-data-services/edit-and-delete-an-entity-sync-relationship-master-data-services.md)  
  
  
