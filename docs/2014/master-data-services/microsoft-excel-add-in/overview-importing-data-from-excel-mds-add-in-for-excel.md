---
title: Pubblicazione dei dati (aggiuntivo MDS per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: ea84a9aa-aeec-411b-ab8d-bc1b14f864a3
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: dd5046c9a307f498ffb585c99cba8044c7b18b3f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65479037"
---
# <a name="publishing-data-mds-add-in-for-excel"></a>Pubblicazione dei dati (componente aggiuntivo MDS per Excel)
  In [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]pubblicare i dati nel repository MDS per condividerlo con altri utenti. Appena i dati vengono pubblicati, sono disponibili per essere scaricati dagli altri utenti del componente aggiuntivo.  
  
 Quando si pubblicano dati, tutti i dati aggiunti o aggiornati vengono pubblicati nel repository MDS. I dati eliminati non vengono pubblicati; i dati devono essere eliminati separatamente. Per altre informazioni, vedere [Eliminare una riga &#40;componente aggiuntivo MDS per Excel&#41;](delete-a-row-mds-add-in-for-excel.md).  
  
> [!NOTE]  
>  La pubblicazione non può essere utilizzata per creare una nuova entità. Per altre informazioni sulla creazione di entità, vedere [Creare un'entità &#40;componente aggiuntivo MDS per Excel&#41;](create-an-entity-mds-add-in-for-excel.md).  
  
## <a name="when-multiple-users-publish-at-the-same-time"></a>Quando più utenti pubblicano contemporaneamente  
 Più utenti possono pubblicare aggiornamenti agli stessi dati. Appena ogni utente pubblica dati, l'aggiornamento viene salvato nel database. Pertanto, un utente che non sta utilizzando i dati aggiornati più di recente può ancora modificare il valore quando li pubblica.  
  
 Solo gli aggiornamenti apportati vengono pubblicati nel database. Tutti i dati non aggiornati nel foglio di lavoro non vengono pubblicati.  
  
## <a name="transactions-and-annotations"></a>Transazioni e annotazioni  
 Ogni modifica pubblicata viene salvata come una transazione. Se lo si desidera, è possibile aggiungere annotazioni (commenti) a una transazione per spiegare il motivo della modifica apportata.  
  
-   Non è possibile annotare eliminazioni, anche se le eliminazioni vengono salvate come transazioni che possono essere annullate da un amministratore.  
  
-   Se si modifica il **codice** valore per un membro, non viene registrato come una transazione e non sono disponibili tutte le transazioni precedenti per il membro.  
  
-   È possibile visualizzare le transazioni effettuate per un membro dagli altri utenti. È possibile visualizzare anche tutte le transazioni effettuate per un membro, anche se non si dispone più delle autorizzazioni per specifici attributi.  
  
 È possibile visualizzare tutte le transazioni effettuate per un membro. Per altre informazioni, vedere [Visualizzare tutte le annotazioni o transazioni per un membro &#40;componente aggiuntivo MDS per Excel&#41;](view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md).  
  
> [!IMPORTANT]  
>  Se si immette un'annotazione con una lunghezza superiore a 500 caratteri, l'annotazione viene troncata automaticamente.  
  
## <a name="business-rule-and-other-validation"></a>Regola business e altre convalide  
 Quando si pubblicano dati, la convalida viene eseguita per assicurare che i dati siano esatti prima di aggiungerli al repository MDS. Se i dati non soddisfano i criteri specificati, non verranno pubblicati nel repository. Per altre informazioni, vedere [Convalida dei dati &#40;componente aggiuntivo MDS per Excel&#41;](validating-data-mds-add-in-for-excel.md).  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Pubblicare dati dal foglio di lavoro attivo nel repository MDS.|[Pubblicare dati da Excel a MDS &#40;componente aggiuntivo MDS per Excel&#41;](import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)|  
|Eliminare contemporaneamente una riga dal repository MDS e dal foglio di lavoro.|[Eliminare una riga &#40;componente aggiuntivo MDS per Excel&#41;](delete-a-row-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   [Aggiornamento dei dati &#40;Componente aggiuntivo MDS per Excel&#41;](refreshing-data-mds-add-in-for-excel.md)  
  
-   [Componente aggiuntivo Master Data Services per Microsoft Excel](master-data-services-add-in-for-microsoft-excel.md)  
  
  
