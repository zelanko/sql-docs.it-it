---
title: Aggiungere un tipo di contenuto connessione BI Semantic Model a una raccolta (PowerPivot per SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 145505ed-50bc-4528-912b-2a5cd2566011
author: minewiskan
ms.author: owend
ms.openlocfilehash: 8535458f61b57440859879151c4fcad24846d7e0
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547653"
---
# <a name="add-a-bi-semantic-model-connection-content-type-to-a-library-powerpivot-for-sharepoint"></a>Aggiungere un tipo di contenuto connessione BISM (BI Semantic Model) a una raccolta (PowerPivot per SharePoint)
  Una connessione BISM viene creata in SharePoint e fornisce il reindirizzamento ai dati Business Intelligence Semantic Model in una cartella di lavoro di PowerPivot o un database modello tabulare di Analysis Services in un server di rete. Prima di creare una connessione BISM in SharePoint, è necessario estendere una raccolta documenti per consentire la creazione di un file con estensione bism. Questo passaggio deve essere eseguito solo una volta per ogni raccolta, tuttavia sarà necessario ripeterlo per qualsiasi raccolta da cui si desidera creare file con estensione bism. In base alle procedure consigliate, è opportuno creare una raccolta centralizzata per l'archiviazione di file con estensione bism in modo da poter gestire le autorizzazioni da un'unica posizione.  
  
> [!NOTE]  
>  Se si utilizzano già raccolte connessioni dati SharePoint, il tipo di contenuto della connessione BISM viene aggiunto automaticamente a tale modello di raccolta. È possibile ignorare i passaggi descritti in questa sezione se si utilizza una raccolta connessioni dati che consente già di creare nuovi documenti di connessione BISM.  
  
##  <a name="add-the-content-type-to-a-document-library"></a><a name="bkmk_addtype"></a> Aggiungere il tipo di contenuto a una raccolta documenti  
 È necessario disporre almeno dell'autorizzazione Gestione elenchi per aggiungere e configurare un tipo di contenuto. Questa autorizzazione viene compilata nel livello di autorizzazione Progettazione e superiore.  
  
 Nel sito che contiene la raccolta documenti deve essere configurata l'attivazione della funzionalità per PowerPivot per SharePoint. Per ulteriori informazioni, vedere [attivazione dell'integrazione delle funzionalità di PowerPivot per le raccolte siti in Amministrazione centrale](activate-power-pivot-integration-for-site-collections-in-ca.md).  
  
1.  Aprire la raccolta documenti per cui si desidera abilitare il tipo di contenuto della connessione BISM.  
  
2.  Sulla barra multifunzione di SharePoint, in Strumenti raccolta fare clic su **Raccolta**.  
  
3.  Fare clic su **Impostazioni raccolta**.  
  
4.  In Impostazioni generali scegliere **Impostazioni avanzate**.  
  
5.  In Tipi di contenuto nella sezione "Consenti la gestione di più tipi di contenuto:" scegliere **Sì**.  
  
6.  Fare clic su **OK**.  
  
7.  Nella sezione Tipi di contenuto fare clic su **Aggiungi da tipi di contenuto del sito esistenti**. Se questa pagina non viene visualizzata, tornare al sito, fare clic su **Raccolta** in Strumenti raccolta, quindi scegliere **Impostazioni raccolta**.  
  
8.  In Tipi di contenuto fare clic su **Aggiungi da tipi di contenuto del sito esistenti**.  
  
9. In Seleziona tipi di contenuto del sito da: scegliere **Business Intelligence**.  
  
10. In Tipi di contenuto del sito disponibili selezionare **File di connessione BISM**, quindi scegliere **Aggiungi** per spostare il tipo di contenuto selezionato nell'elenco Tipi di contenuto da aggiungere.  
  
11. Fare clic su **OK**.  
  
12. Per verificare l'aggiunta del tipo di contenuto, tornare alla raccolta e fare clic su **Nuovo documento** nell'area Documenti della barra multifunzione della raccolta. Nell'elenco Nuovi documenti dovrebbe essere presente **File di connessione BISM** .  
  
     ![Sottomenu Nuovo documento in una raccolta di SharePoint](../media/ssas-bismconnection-new.gif "Sottomenu Nuovo documento in una raccolta di SharePoint")  
  
 Dopo avere abilitato il tipo di contenuto della connessione BISM per una raccolta, è possibile creare una connessione che fornisce il reindirizzamento ai dati BISM che possono essere utilizzati da report di Excel o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] . Per ulteriori informazioni su questa operazione, utilizzare i collegamenti seguenti:  
  
 [Creare una connessione BISM (BI Semantic Model) a una cartella di lavoro di PowerPivot](create-a-bi-semantic-model-connection-to-a-power-pivot-workbook.md)  
  
 [Creare una connessione BISM a un database modello tabulare](create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Connessione BI Semantic Model di PowerPivot &#40;. BISM&#41;](power-pivot-bi-semantic-model-connection-bism.md)   
 [Utilizzare una connessione BISM (BI Semantic Model) in Excel o Reporting Services](use-a-bi-semantic-model-connection-in-excel-or-reporting-services.md)  
  
  
