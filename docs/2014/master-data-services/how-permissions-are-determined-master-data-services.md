---
title: Modalità di determinazione delle autorizzazioni (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- permissions [Master Data Services], determining permissions
ms.assetid: 1dc0b43a-d023-4e7d-b027-8b1459fd058c
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 90c6aaed02e2dbbb39ddae605280d5ee00d28548
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971431"
---
# <a name="how-permissions-are-determined-master-data-services"></a>Modalità di determinazione delle autorizzazioni (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]il modo più semplice per configurare la sicurezza consiste nell'assegnare autorizzazioni per oggetti modello a un gruppo di cui l'utente è membro.

 La sicurezza diventa più complessa quando:

-   Vengono assegnate entrambe le autorizzazioni per oggetti modello e membri gerarchia.

-   L'utente appartiene a gruppi e le autorizzazioni vengono assegnate sia all'utente sia ai gruppi.

-   L'utente appartiene a gruppi e le autorizzazioni vengono assegnate a più gruppi.

## <a name="permissions-assigned-to-a-single-group-or-user"></a>Autorizzazioni assegnate a un singolo gruppo o utente
 Se vengono assegnate a un singolo gruppo o utente, le autorizzazioni vengono determinate in base al flusso di lavoro seguente.

 ![mds_conc_security_no_overlap](../../2014/master-data-services/media/mds-conc-security-no-overlap.gif "mds_conc_security_no_overlap")

### <a name="step-1-effective-attribute-permissions-are-determined"></a>Passaggio 1: vengono determinate le autorizzazioni per attributi valide.
 Nell'elenco seguente viene descritto il modo in cui vengono determinate le autorizzazioni per attributi valide:

-   Le autorizzazioni assegnate agli oggetti modello determinano gli attributi a cui un utente può accedere.

-   Tutti gli oggetti modello ereditano automaticamente le autorizzazioni dall'oggetto più vicino a un livello superiore della struttura del modello.

-   Tutti gli oggetti che si trovano allo stesso livello dell'entità vengono negati in modo implicito.

-   A tutti gli oggetti che si trovano a un livello superiore viene fornito l'accesso per la navigazione. Per ulteriori informazioni sull'accesso per la navigazione, vedere [accesso &#40;Master Data Services&#41;](navigational-access-master-data-services.md).

 In questo esempio, l'autorizzazione di sola **lettura** viene assegnata a un'entità e tale autorizzazione viene ereditata dal relativo attributo, che è a un livello inferiore della struttura del modello. Il modello fornisce l'accesso per la navigazione a questa entità e al relativo attributo. All'altra entità del modello non viene assegnata alcuna autorizzazione esplicita e non eredita alcuna autorizzazione, pertanto viene negata in modo implicito.

 ![mds_conc_inheritance_model](../../2014/master-data-services/media/mds-conc-inheritance-model.gif "mds_conc_inheritance_model")

### <a name="step-2-if-hierarchy-member-permissions-are-assigned-effective-member-permissions-are-determined"></a>Passaggio 2: Se vengono assegnate le autorizzazioni per i membri gerarchia, vengono determinate le autorizzazioni per i membri valide.
 Nell'elenco seguente viene descritto il modo in cui vengono determinate le autorizzazioni per i membri gerarchia valide:

-   Le autorizzazioni assegnate ai nodi gerarchia determinano i membri a cui un utente può accedere.

-   Tutti i nodi di una gerarchia ereditano automaticamente le autorizzazioni dall'oggetto più vicino a un livello superiore della struttura della gerarchia.

-   Tutti i nodi che si trovano allo stesso livello vengono negati in modo implicito.

-   Tutti i nodi che si trovano a livelli superiori a cui non sono assegnate autorizzazioni vengono negati in modo implicito.

 In questo esempio, l'autorizzazione di sola **lettura** viene assegnata a un nodo della gerarchia e tale autorizzazione viene ereditata da un nodo a un livello inferiore della struttura della gerarchia. Alla radice non viene assegnata alcuna autorizzazione, pertanto viene negata in modo implicito. All'altro nodo della struttura della gerarchia non viene assegnata alcuna autorizzazione esplicita e non eredita alcuna autorizzazione, pertanto viene negato in modo implicito.

 ![mds_conc_inheritance_hierarchy](../../2014/master-data-services/media/mds-conc-inheritance-hierarchy.gif "mds_conc_inheritance_hierarchy")

### <a name="step-3-the-intersection-of-attribute-and-member-permissions-is-determined"></a>Passaggio 3: viene determinata l'intersezione delle autorizzazioni per membri e attributi.
 Se le autorizzazioni per attributi valide sono diverse dalle autorizzazioni per membri valide, le autorizzazioni devono essere determinate per ogni singolo valore di attributo. Per altre informazioni, vedere [Autorizzazioni per modelli e membri sovrapposte &#40;Master Data Services&#41;](../../2014/master-data-services/overlapping-model-and-member-permissions-master-data-services.md).

## <a name="permissions-assigned-to-multiple-groups"></a>Autorizzazioni assegnate a più gruppi
 Se un utente appartiene uno o più gruppi e le autorizzazioni vengono assegnate sia all'utente sia ai gruppi, il flusso di lavoro diventa più complesso.

 ![mds_conc_security_group_overlap](../../2014/master-data-services/media/mds-conc-security-group-overlap.gif "mds_conc_security_group_overlap")

 In questo caso, la sovrapposizione delle autorizzazioni utente e gruppo deve essere risolta prima del confronto tra autorizzazioni per membri gerarchia e oggetti modello. Per altre informazioni, vedere [Autorizzazioni utenti e gruppi sovrapposte &#40;Master Data Services&#41;](../../2014/master-data-services/overlapping-user-and-group-permissions-master-data-services.md).

## <a name="see-also"></a>Vedere anche
 [Autorizzazioni per utenti e gruppi sovrapposte &#40;Master Data Services&#41;](../../2014/master-data-services/overlapping-user-and-group-permissions-master-data-services.md) [autorizzazioni per modelli e membri sovrapposte &#40;Master Data Services&#41;](../../2014/master-data-services/overlapping-model-and-member-permissions-master-data-services.md)


