---
title: Sicurezza (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 56bc41ea-de28-4184-aa7e-99111ae55af5
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: ee6fd4fbf047ecb29dae4f35fe3bbbf5a3f9da61
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62923196"
---
# <a name="security-master-data-services"></a>Sicurezza (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]utilizzare la sicurezza per assicurare che agli utenti sia consentito l'accesso ai dati master specifici necessari per l'esecuzione dei processi e per impedire l'accesso ai dati che non devono essere loro disponibili.  
  
 È possibile utilizzare anche la sicurezza per creare un amministratore di un modello specifico e un'area funzionale (ad esempio, per consentire a qualcuno di creare versioni del modello Customer o per dare la possibilità di impostare autorizzazioni di sicurezza).  
  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] è basata su utenti e gruppi locali o del dominio Active Directory. La sicurezza MDS consente all'utente di utilizzare un livello di dettaglio granulare durante l'individuazione dei dati ai quali un utente può accedere. A causa della granularità, la sicurezza può diventare facilmente complicata ed è necessario prestare attenzione durante l'utilizzo di utenti e gruppi sovrapposti. Per altre informazioni, vedere [Autorizzazioni utenti e gruppi sovrapposte &#40;Master Data Services&#41;](overlapping-user-and-group-permissions-master-data-services.md).  
  
 È possibile assegnare l'accesso di sicurezza nell'area funzionale **Autorizzazioni utenti e gruppi** dell'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] o tramite il servizio Web.  
  
## <a name="types-of-users"></a>Tipi di utenti  
 Esistono due tipi di utenti in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]:  
  
-   Quelli che accedono ai dati nell'area funzionale **Esplora risorse** .  
  
-   Quelli che dispongono della possibilità di eseguire attività amministrative in aree diverse da **Esplora risorse**. Questi utenti sono chiamati [Administrators &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md).  
  
## <a name="how-to-set-security"></a>Impostazione della sicurezza  
 Per concedere ad un utente o gruppo l'autorizzazione di accesso a dati o a funzionalità in MDS, è necessario assegnare:  
  
-   L'[accesso all'area funzionale](../../2014/master-data-services/functional-area-permissions-master-data-services.md), che determina a quali delle cinque aree funzionali dell'interfaccia utente un utente può accedere.  
  
-   [Autorizzazioni per oggetti modello](../../2014/master-data-services/model-object-permissions-master-data-services.md)che determinano gli attributi ai quali un utente può accedere e il tipo di accesso (lettura o aggiornamento) che l'utente possiede su quegli attributi.  
  
-   Facoltativamente, le [autorizzazioni per i membri della gerarchia](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)che determinano i membri ai quali un utente può accedere e il tipo di accesso (lettura o aggiornamento) che l'utente possiede su quei membri.  
  
 Quando si assegnano le autorizzazioni a attributi e membri, le autorizzazioni si intersecano e le regole determinano quale autorizzazione ha la precedenza. Per altre informazioni, vedere [Modalità di determinazione delle autorizzazioni &#40;Master Data Services&#41;](../../2014/master-data-services/how-permissions-are-determined-master-data-services.md).  
  
 Per implementare la sicurezza a livello di record, creare una gerarchia per un'entità e assegnare le autorizzazioni utente ai membri della gerarchia. I membri sono record di dati.  Le autorizzazioni membri gerarchia devono essere usate solo quando si vuole che un utente abbia accesso limitato a membri specifici.  
  
 La figura seguente mostra la gerarchia derivata per l'entità Style e le autorizzazioni dei membri Style per un utente selezionato. Le autorizzazioni per l'aggiornamento vengono assegnate ai membri M {Men's} e U {Unisex} e le autorizzazioni di sola lettura vengono assegnate al membro con stile "Women's". L'utente potrà quindi aggiornare i record per i prodotti di tipo "Men's" e "Unisex" e potrà solo leggere i record per i prodotti con stile di tipo "Women's".  
  
 ![Applicare uno stile a gerarchie derivate e membri le autorizzazioni](../../2014/master-data-services/media/style-derived-hierarchy-mds.png "autorizzazioni gerarchia derivata di stile e membri")  
  
 Per informazioni su come creare una gerarchia, vedere [creare una gerarchia esplicita &#40;Master Data Services&#41; ](../../2014/master-data-services/create-an-explicit-hierarchy-master-data-services.md) e [creare una gerarchia derivata &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-derived-hierarchy-master-data-services.md).  
  
 Per informazioni su come assegnare membri le autorizzazioni, vedere [assegnare autorizzazioni membri gerarchia &#40;Master Data Services&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)  
  
## <a name="security-in-the-add-in-for-excel"></a>Sicurezza nel componente aggiuntivo di Excel  
 La sicurezza impostata nell'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] viene anche applicata a [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]. Gli utenti possono visualizzare e utilizzare solo i dati per cui dispongono dell'autorizzazione. Gli amministratori possono eseguire attività amministrative.  
  
 L'unico problema è che tutta la sicurezza assegnata in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] diventa effettiva in Excel solo dopo un periodo di tempo di 20 minuti. Tale intervallo viene definito dall'impostazione *MdsMaximumUserInformationCacheInterval* nel file web.config. Per modificare l'intervallo, modificare l'impostazione e riavviare IIS.  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Creare un utente che dispone delle autorizzazioni complete per un modello.|[Creare un amministratore di modelli &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-model-administrator-master-data-services.md)|  
|Aggiungere un gruppo Active Directory a [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]; questo è il primo passaggio nell'assegnazione di un'autorizzazione al gruppo per accedere ai dati nell'applicazione Web [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|[Aggiungere un gruppo &#40;Master Data Services&#41;](../../2014/master-data-services/add-a-group-master-data-services.md)|  
|Assegnare l'autorizzazione a un'area funzionale dell'applicazione Web [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|[Assegnare autorizzazioni per aree funzionali &#40;Master Data Services&#41;](../../2014/master-data-services/assign-functional-area-permissions-master-data-services.md)|  
|Assegnare l'autorizzazione ai valori dell'attributo assegnando l'autorizzazione agli oggetti modello.|[Assegnare autorizzazioni per oggetti modello &#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)|  
|Assegnare l'autorizzazione ai valori del membro assegnando l'autorizzazione ai nodi della gerarchia.|[Assegnare autorizzazioni membri gerarchia &#40;Master Data Services&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Amministratori &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md)   
 [Utenti e gruppi &#40;Master Data Services&#41;](../../2014/master-data-services/users-and-groups-master-data-services.md)   
 [Autorizzazioni per aree funzionali &#40;Master Data Services&#41;](../../2014/master-data-services/functional-area-permissions-master-data-services.md)   
 [Autorizzazioni per oggetti modello &#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [Autorizzazioni membri gerarchie &#40;Master Data Services&#41;](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [Modalità di determinazione delle autorizzazioni &#40;Master Data Services&#41;](../../2014/master-data-services/how-permissions-are-determined-master-data-services.md)  
  
  
