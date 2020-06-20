---
title: Gerarchie esplicite (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- explicit hierarchies, about explicit hierarchies
- hierarchies [Master Data Services], explicit hierarchies
- explicit hierarchies
ms.assetid: e6f44e37-e1f0-4c38-a816-1935a856d5a4
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: c83528f45c6c4174f7714a5f22d8757de4e4fda2
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971491"
---
# <a name="explicit-hierarchies-master-data-services"></a>Gerarchie esplicite (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]una gerarchia esplicita consente di organizzare i membri di una sola entità secondo qualsiasi modalità specificata. La struttura può essere incompleta e, a differenza delle gerarchie derivate, le gerarchie esplicite non sono basate su relazioni tra attributi basati su dominio.

## <a name="consolidated-members-group-other-members"></a>Membri consolidati che raggruppano altri membri
 In una gerarchia esplicita vengono utilizzati membri consolidati creati allo scopo di raggruppare altri membri. Questi membri consolidati possono appartenere a un'unica gerarchia esplicita per volta. Inoltre, in una gerarchia esplicita sono inclusi tutti i membri foglia dell'entità associata.

 Una gerarchia esplicita può essere incompleta, il che vuol dire che la gerarchia può terminare su livelli diversi simultaneamente. Ogni membro consolidato può disporre di un numero illimitato di membri consolidati e foglia sottostanti oppure di nessuno membro. I membri foglia possono trovarsi al di sotto di un singolo membro consolidato o al di sotto di più livelli di membri consolidati.

> [!NOTE]
>  Prima di creare una gerarchia esplicita, è necessario abilitare l'entità per le gerarchie esplicite. Per altre informazioni, vedere [abilitare un'entità per gerarchie esplicite e raccolte &#40;Master Data Services&#41;](enable-an-entity-for-explicit-hierarchies-and-collections-master-data-services.md).

## <a name="types-of-explicit-hierarchies"></a>Tipi di gerarchie esplicite
 Esistono due tipi di gerarchie esplicite, ovvero obbligatoria e non obbligatoria.

### <a name="mandatory-explicit-hierarchy"></a>Gerarchia esplicita obbligatoria
 Una gerarchia esplicita obbligatoria è una gerarchia nella quale tutti i membri foglia devono essere inclusi nell'albero gerarchico. Per impostazione predefinita, tutti i membri vengono inclusi al livello radice dell'albero. È possibile ridisporre i membri in base alle necessità.

### <a name="non-mandatory-explicit-hierarchy"></a>Gerarchia esplicita non obbligatoria
 Una gerarchia esplicita non obbligatoria è una gerarchia nella quale tutti i membri foglia si trovano in un nodo **Inutilizzato** creato dal sistema. I membri necessari possono essere spostati fuori da questo nodo. Il resto dei membri può rimanere nel nodo **Inutilizzato** .

 Quando si utilizzano gerarchie esplicite non obbligatorie, le attività di report o le analisi eseguite sulla gerarchia potrebbero non corrispondere alle attività di report o analisi eseguite su gerarchie obbligatorie.

## <a name="rules"></a>Regole
 Le regole seguenti si applicano alle gerarchie esplicite (obbligatorie e non obbligatorie).

-   Ogni membro foglia può essere incluso nella gerarchia una sola volta.

-   Tutti i membri consolidati devono essere inclusi in una gerarchia.

-   I membri consolidati non possono trovarsi in più di una gerarchia esplicita.

-   I membri consolidati nell'albero gerarchico non devono contenere membri foglia sottostanti.

-   Se si elimina una gerarchia esplicita, vengono eliminati tutti i membri consolidati utilizzati nella gerarchia.

-   Se si elimina un membro consolidato incluso in una gerarchia esplicita, tutti i membri foglia raggruppati in base a tale membro consolidato vengono spostati al livello radice.

## <a name="explicit-hierarchies-versus-derived-hierarchies"></a>Gerarchie esplicite e gerarchie derivate
 Nella tabella seguente vengono illustrate alcune differenze tra le gerarchie esplicite e derivate.

|Gerarchie esplicite|Gerarchie derivate|
|--------------------------|-------------------------|
|La struttura viene definita dall'utente|La struttura è derivata dalle relazioni tra attributi basati su dominio|
|Contengono membri di una sola entità|Contengono membri di più entità|
|Utilizzano i membri consolidati per raggruppare altri membri|Utilizzano i membri foglia di un'entità per raggruppare i membri foglia di un'altra entità|
|Possono essere incomplete|Contengono sempre un numero coerente di livelli|

## <a name="explicit-hierarchy-example"></a>Esempio di gerarchia esplicita
 Nell'esempio seguente, l'entità Product contiene i seguenti membri foglia: BK-M101 {Mountain-100}, BK-M201 {Mountain-200}, BK-M301 {Mountain-300}, BK-R150 {Road-150}, BK-R450 {Road-450} e BK-R650 {Road-650}.

 Per riepilogare i membri foglia in corrispondenza di punti di consolidamento specifici, è possibile creare membri consolidati nell'entità Product. Inserire i membri consolidati nei livelli dell'albero gerarchico nel punto in cui si desidera riepilogare i membri foglia. Non sussistono limitazioni rispetto al punto di inserimento dei membri consolidati. Ogni membro (foglia o consolidato) può tuttavia essere utilizzato una sola volta.

 ![Esempio di gerarchia esplicita di mountain bike](../../2014/master-data-services/media/mds-conc-explicit-hierarchy.gif "Esempio di gerarchia esplicita di mountain bike")

 I membri consolidati possono essere utilizzati per raggruppare membri a qualsiasi livello e i membri consolidati vengono ordinati nell'ordine determinato dall'utente.

## <a name="related-tasks"></a>Attività correlate

|Descrizione dell'attività|Argomento|
|----------------------|-----------|
|Abilitare un'entità per le gerarchie esplicite e le raccolte.|[Abilitare un'entità per le gerarchie esplicite e le raccolte &#40;Master Data Services&#41;](enable-an-entity-for-explicit-hierarchies-and-collections-master-data-services.md)|
|Creare una nuova gerarchia esplicita.|[Creare una gerarchia esplicita &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-explicit-hierarchy-master-data-services.md)|
|Modificare il nome di una gerarchia esplicita esistente.|[Modificare il nome di una gerarchia esplicita &#40;Master Data Services&#41;](../../2014/master-data-services/change-an-explicit-hierarchy-name-master-data-services.md)|
|Eliminare una gerarchia esplicita esistente.|[Eliminare una gerarchia esplicita &#40;Master Data Services&#41;](../../2014/master-data-services/delete-an-explicit-hierarchy-master-data-services.md)|
|||

## <a name="related-content"></a>Contenuto correlato

-   [Gerarchie derivate &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-master-data-services.md)

-   [Raccolte &#40;Master Data Services&#41;](../../2014/master-data-services/collections-master-data-services.md)


