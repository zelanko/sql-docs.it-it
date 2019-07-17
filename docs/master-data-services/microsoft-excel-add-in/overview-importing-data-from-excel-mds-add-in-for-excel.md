---
title: Panoramica Importazione di dati da Excel (aggiuntivo MDS per Excel) | Microsoft Docs
ms.custom: microsoft-excel-add-in
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: ea84a9aa-aeec-411b-ab8d-bc1b14f864a3
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 1da9e1876995f81fd2b40b9ef1bb4b509b4c848d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68074479"
---
# <a name="overview-importing-data-from-excel-mds-add-in-for-excel"></a>Panoramica Importazione dei dati da Excel (Componente aggiuntivo Master Data Services per Microsoft Excel)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]pubblicare i dati nel repository MDS per condividerlo con altri utenti. Appena i dati vengono pubblicati, sono disponibili per essere scaricati dagli altri utenti del componente aggiuntivo.  
  
 Quando si pubblicano dati, tutti i dati aggiunti o aggiornati vengono pubblicati nel repository MDS. I dati eliminati non vengono pubblicati; i dati devono essere eliminati separatamente. Per altre informazioni, vedere [Eliminare una riga &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/delete-a-row-mds-add-in-for-excel.md).  
  
> [!NOTE]  
>  La pubblicazione non può essere utilizzata per creare una nuova entità. Per altre informazioni sulla creazione di entità, vedere [Creare un'entità &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/create-an-entity-mds-add-in-for-excel.md).  
  
## <a name="when-multiple-users-publish-at-the-same-time"></a>Quando più utenti pubblicano contemporaneamente  
 Più utenti possono pubblicare aggiornamenti agli stessi dati. Appena ogni utente pubblica dati, l'aggiornamento viene salvato nel database. Pertanto, un utente che non sta utilizzando i dati aggiornati più di recente può ancora modificare il valore quando li pubblica.  
  
 Solo gli aggiornamenti apportati vengono pubblicati nel database. Tutti i dati non aggiornati nel foglio di lavoro non vengono pubblicati.  
  
## <a name="transactions-and-annotations"></a>Transazioni e annotazioni  
 Ogni modifica pubblicata viene salvata come una transazione. Se lo si desidera, è possibile aggiungere annotazioni (commenti) a una transazione per spiegare il motivo della modifica apportata.  
  
-   Non è possibile annotare eliminazioni, anche se le eliminazioni vengono salvate come transazioni che possono essere annullate da un amministratore.  
  
-   Se si modifica il valore **Code** per un membro, tutte le transazioni precedenti per il membro non sono disponibili. Se si ripristina il valore **Code** al valore originale, è possibile accedere alle transazioni precedenti.  
  
-   È possibile visualizzare le transazioni effettuate per un membro dagli altri utenti. È possibile visualizzare anche tutte le transazioni effettuate per un membro, anche se non si dispone più delle autorizzazioni per specifici attributi. Non è possibile visualizzare le transazioni che interessano gli attributi in cui l'autorizzazione è impostata su Nega.  
  
 È possibile visualizzare tutte le transazioni effettuate per un membro. Per altre informazioni, vedere [Visualizzare tutte le annotazioni o transazioni per un membro &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md).  
  
> [!IMPORTANT]  
>  Se si immette un'annotazione con una lunghezza superiore a 500 caratteri, l'annotazione viene troncata automaticamente.  
  
## <a name="business-rule-and-other-validation"></a>Regola business e altre convalide  
 Quando si pubblicano dati, la convalida viene eseguita per assicurare che i dati siano esatti prima di aggiungerli al repository MDS. Se i dati non soddisfano i criteri specificati, non verranno pubblicati nel repository. Per altre informazioni, vedere [Convalida dei dati &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/validating-data-mds-add-in-for-excel.md).  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Pubblicare dati dal foglio di lavoro attivo nel repository MDS.|[Importare dati da Excel in Master Data Services &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)|  
|Eliminare contemporaneamente una riga dal repository MDS e dal foglio di lavoro.|[Eliminare una riga &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/delete-a-row-mds-add-in-for-excel.md)|  
|Per visualizzare gli aggiornamenti dei dati nel corso del tempo, visualizzare le annotazioni (commenti) e le transazioni per righe di dati (membri).|[Visualizzare tutte le annotazioni o transazioni per un membro &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)|  
|Combinare i dati di due fogli di lavoro per confrontare i dati prima della pubblicazione.|[Combinare i dati &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/combine-data-mds-add-in-for-excel.md)|  

  
## <a name="related-content"></a>Contenuto correlato  
  
-   [Aggiornamento dei dati &#40;Componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/refreshing-data-mds-add-in-for-excel.md)  
  
-   [Componente aggiuntivo Master Data Services per Microsoft Excel](../../master-data-services/microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md)  
  
  
