---
title: Operatori di filtro (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 27914c8b-8951-4b7d-914d-1cbf528dd248
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 5d94a453e9eb5794bdd534f7aaf37ca2e1cc3177
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "65483873"
---
# <a name="filter-operators-master-data-services"></a>Operatori di filtro (Master Data Services)
  Per filtrare un elenco di membri, sono disponibili gli operatori seguenti.  
  
> [!NOTE]  
>  Quando si filtrano in base a più criteri, tutti i criteri devono essere true per restituite i risultati. Ad esempio, SquareFeet = 2000 **AND** Divisione <> 123.  
  
## <a name="filter-operators"></a>Operatori di filtro  
  
|Nome del controllo|Descrizione|  
|------------------|-----------------|  
|**È uguale a**|Restituisce i valori di attributo che corrispondono esattamente ai criteri specificati. Ad esempio, per filtrare in base a **Mountain-100**, è necessario digitare **Mountain-100**.|  
|**È diverso da**|Restituisce i valori di attributo che non corrispondono esattamente ai criteri specificati. I criteri di filtro devono corrispondere esattamente al valore di attributo che si desidera omettere dai risultati. Ad esempio, per omettere i risultati che corrispondono a **Mountain-100**, è necessario digitare **Mountain-100**.<br /><br /> Nota: quando si applica una condizione di filtro con una clausola "È diverso da" su un attributo, un membro per il quale l'attributo è NULL supererà la condizione di filtro e verrà restituito se SET ANSI_NULLS è impostato su ON nelle impostazioni del database. Per arrestare questo comportamento, disattivare SET ANSI_NULLS nelle impostazioni del database. Quando l'opzione SET ANSI_NULLS è impostata su OFF, dai confronti di tutti i dati con un valore Null verrà restituito TRUE, se il valore dei dati è NULL, con il risultato che il membro non supera la clausola "È diverso da". Per altre informazioni, vedere [SET ANSI_NULLS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-nulls-transact-sql).|  
|**È simile a**|Consente di utilizzare l'operatore LIKE di Transact-SQL per filtrare i risultati. Per altre informazioni, vedere la sezione [LIKE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/like-transact-sql) nella documentazione online di SQL Server.|  
|**Non è simile a**|Consente di utilizzare l'operatore NOT di Transact-SQL per filtrare i risultati. Per altre informazioni, vedere la sezione [NOT &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/not-transact-sql) nella documentazione online di SQL Server.|  
|**È maggiore di**|Restituisce i valori di attributo che sono maggiori dei criteri specificati. Ad esempio, per restituire i valori di attributo che iniziano con una lettera maggiore di **F**, digitare **F**.|  
|**È minore di**|Restituisce i valori di attributo che sono minori dei criteri specificati. Ad esempio, per restituire i valori di attributo che iniziano con una lettera minore di **F**, digitare **F**.|  
|**È maggiore o uguale a**|Restituisce i valori di attributo che sono maggiori o uguali ai criteri specificati. Ad esempio, per restituire i valori di attributo che iniziano con **3** o un numero maggiore, digitare **3**.|  
|**È minore o uguale a**|Restituisce i valori di attributo che sono minori o uguali ai criteri specificati. Ad esempio, per restituire i valori di attributo che iniziano con **3** o un numero minore, digitare **3**.|  
|**Corrisponde**|Consente di utilizzare un indice di ricerca fuzzy per filtrare i risultati.<br /><br /> Usare il campo **Livello di somiglianza** per specificare il livello di corrispondenza dei valori degli attributi ai criteri di filtro. L'impostazione predefinita è 30%. Selezionare una delle opzioni seguenti nell'elenco a discesa **Algoritmo** :<br /><br /> **Levenshtein**: distanza basata sul numero di modifiche (ad esempio, aggiunte o eliminazioni) accettate dall'algoritmo per la corrispondenza tra stringhe. Questa è la modalità predefinita. Non è richiesto alcun parametro aggiuntivo.<br /><br /> **Jaccard**: indice il cui funzionamento è ottimale quando si tenta di far corrispondere più stringhe. Questa ricerca supporta un parametro aggiuntivo di distorsione contenimento (vedere di seguito).<br /><br /> **Jaro-Winkler**: distanza utilizzata meglio per l'individuazione di nomi di persona duplicati. Tramite questo metodo vengono restituiti più risultati rispetto a qualsiasi altro metodo. Non supporta la distorsione contenimento.<br /><br /> **Sottosequenza comune più estesa**: funziona in base a una sottosequenza nella quale le lettere in un modello vengono visualizzate in ordine, anche se possono essere separate (ad esempio, "MSR" è una sottosequenza di "Master"). Questa ricerca supporta un parametro aggiuntivo di distorsione contenimento (vedere di seguito).<br /><br /> <br /><br /> per l'algoritmo **Jaccard** o **Sottosequenza comune più lunga** aggiungere **Distorsione contenimento**. **Distorsione contenimento** è una soglia di lunghezza fornita in una percentuale decimale compresa tra 0 e 1, con 0,62 come valore predefinito. Una soglia inferiore comporterà l'aumento del numero di corrispondenze possibili restituite.|  
|**Non corrisponde a**|Consente di utilizzare un indice di ricerca fuzzy per filtrare i risultati. Utilizzare il campo **Livello di somiglianza** per determinare il grado di non corrispondenza dei valori di attributo ai criteri di filtro specificati.|  
|**Contiene il criterio**|Consente di utilizzare espressioni regolari di .NET Framework per filtrare i risultati in base a un modello specificato. Per ulteriori informazioni su espressioni regolari, vedere [Elementi del linguaggio di espressioni regolari](https://go.microsoft.com/fwlink/?LinkId=164401) in MSDN Library.|  
|**Non contiene il modello**|Consente di utilizzare le espressioni regolari di .NET Framework per filtrare i risultati che non corrispondono a un modello specificato. Per ulteriori informazioni su espressioni regolari, vedere [Elementi del linguaggio di espressioni regolari](https://go.microsoft.com/fwlink/?LinkId=164401) in MSDN Library.|  
|**È NULL**|Restituisce i valori di attributo che sono Null. Il campo **Criteri** viene disabilitato quando si seleziona l'operatore **È NULL** .|  
|**Non è NULL**|Restituisce i valori di attributo che non sono null. Il campo **Criteri** viene disabilitato quando si seleziona l'operatore **Non è NULL** .|  
  
  
