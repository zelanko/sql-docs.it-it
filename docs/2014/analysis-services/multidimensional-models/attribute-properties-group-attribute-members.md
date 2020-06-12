---
title: Membri attributo gruppo (discretizzazione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- NameColumn property
- discretization [Analysis Services]
- member groups [Analysis Services]
- grouping members
- DiscretizationNumber property
- sort orders [Analysis Services]
- DiscretizationMethod property
- adding members to member group
- number of member groups
- members [Analysis Services], groups
- names [Analysis Services], member groups
ms.assetid: 5cf2f407-accc-4baf-b54f-7703af338325
author: minewiskan
ms.author: owend
ms.openlocfilehash: 7e2c52ec93b46418b82b681fbacc1d31338a0d88
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544783"
---
# <a name="group-attribute-members-discretization"></a>Raggruppare membri di attributo (discretizzazione)
  Un gruppo di membri è una raccolta generata dal sistema di membri consecutivi di una dimensione. In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] i membri di un attributo possono essere raggruppati in un numero di gruppi di membri tramite un processo denominato discretizzazione. Un livello di una gerarchia contiene gruppi di membri o membri, ma non entrambi. Esplorando un livello contenente gruppi di membri, gli utenti aziendali visualizzano i nomi e i valori delle celle dei gruppi di membri. I membri generati da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per supportare i gruppi di membri vengono denominati membri di raggruppamento e vengono visualizzati come membri ordinari.  
  
 La proprietà `DiscretizationMethod` di un attributo controlla la modalità di raggruppamento dei membri.  
  
|Impostazione di `DiscretizationMethod`|Descrizione|  
|--------------------------------------|-----------------|  
|`None`|Visualizza i membri.|  
|`Automatic`|Seleziona il metodo in grado di rappresentare in modo ottimale i dati, ovvero il metodo `EqualAreas` o il metodo `Clusters`.|  
|`EqualAreas`|Tenta di suddividere i membri dell'attributo in gruppi contenenti un numero uguale di membri.|  
|`Clusters`|Tenta di suddividere i membri dell'attributo in gruppi eseguendo il campionamento dei dati di training, l'inizializzazione su un numero di punti casuali e diverse iterazioni dell'algoritmo di clustering EM (Expectation Maximization).<br /><br /> Questo metodo è utile perché può essere applicato a qualsiasi curva di distribuzione, ma determina tempi di elaborazione più lunghi.|  
  
 La proprietà `DiscretizationNumber` degli attributi specifica il numero di gruppi da visualizzare. Se la proprietà è impostata sul valore predefinito 0, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] determina il numero di gruppi eseguendo il campionamento o la lettura dei dati, in base all'impostazione della proprietà `DiscretizationMethod`.  
  
 L'ordinamento dei membri nei gruppi di membri viene controllato tramite la proprietà `OrderBy` dell'attributo. I membri di un gruppo di membri vengono ordinati consecutivamente in base a tale ordinamento.  
  
 Un utilizzo comune per i gruppi di membri è il drill-down da un livello con pochi membri a uno con molti membri. Per consentire agli utenti il drill-down tra i livelli, cambiare l'impostazione della proprietà `DiscretizationMethod` dell'attributo per il livello contenente numerosi membri da `None` a uno dei metodi di discretizzazione descritti nella tabella precedente. Se una dimensione Client contiene una gerarchia dell'attributo Client Name con 500.000 membri, ad esempio, è possibile rinominare tale attributo Client Groups e impostare la proprietà `DiscretizationMethod` su `Automatic` per visualizzare gruppi di membri al livello dei membri della gerarchia dell'attributo.  
  
 Per eseguire il drill-down ai singoli client in ogni gruppo, è possibile creare un'altra gerarchia dell'attributo Client Name associata alla stessa colonna della tabella. Creare quindi una nuova gerarchia utente basata sui due attributi. Il livello principale sarà basato sull'attributo Client Groups e il livello inferiore sarà basato sull'attributo Client Name. La proprietà `IsAggregatable` sarà `True` per entrambi gli attributi. L'utente potrà quindi espandere il livello (Totale) nella gerarchia per visualizzare i membri del gruppo ed espandere i membri del gruppo per visualizzare i membri foglia della gerarchia. Per nascondere il livello dei gruppi o dei client, è possibile impostare la proprietà `AttributeHierarchyVisible` su `False` per l'attributo corrispondente.  
  
## <a name="naming-template"></a>Modello di denominazione  
 I nomi dei gruppi di membri vengono generati automaticamente alla creazione dei gruppi di membri. Se non viene specificato un modello di denominazione, viene utilizzato il modello di denominazione predefinito. È possibile modificare il metodo di denominazione specificando un modello di denominazione nell'opzione `Format` della proprietà `NameColumn` di un attributo. È possibile ridefinire modelli di denominazione diversi per ogni lingua specificata nella raccolta `Translations` dell'associazione di colonna utilizzata per la proprietà `NameColumn` dell'attributo.  
  
 L'impostazione `Format` determina l'utilizzo dell'espressione stringa seguente per la definizione del modello di denominazione:  
  
 `<Naming template> ::= <First definition> [;<Intermediate definition>;<Last definition>]`  
  
 `<First definition> ::= <Name expression>`  
  
 `<Intermediate definition> ::= <Name expression>`  
  
 `<Last definition> ::= <Name expression>`  
  
 Il parametro `<First definition>` viene applicato soltanto al primo o unico gruppo di membri generato dal metodo di discretizzazione. Se non vengono specificati i parametri facoltativi `<Intermediate definition>` e `<Last definition>` , il parametro `<First definition>` verrà utilizzato per tutti i gruppi di misure generati per l'attributo.  
  
 Il parametro `<Last definition>` viene applicato soltanto all'ultimo gruppo di membri generato dal metodo di discretizzazione.  
  
 Il parametro `<Intermediate bucket name>` viene applicato soltanto a ogni gruppo di membri diverso dal primo o dall'ultimo gruppo di membri generato dal metodo di discretizzazione. Se vengono generati due gruppi di membri o un numero inferiore, questo parametro viene ignorato.  
  
 Il parametro `<Bucket name>` è costituito da un'espressione stringa in cui può essere incorporato un set di variabili per rappresentare informazioni sui membri o sui gruppi di membri nell'ambito del nome del gruppo di membri:  
  
|Variabile|Descrizione|  
|--------------|-----------------|  
|%{First bucket member}|Nome del primo membro da includere nel gruppo di membri corrente.|  
|%{Last bucket member}|Nome dell'ultimo membro da includere nel gruppo di membri corrente.|  
|%{Previous bucket last member}|Nome dell'ultimo membro assegnato al gruppo di membri precedente.|  
|%{Next bucket first member}|Nome del primo membro assegnato al gruppo di membri successivo.|  
|%{Bucket Min}|Valore minimo dei membri da assegnare al gruppo di membri corrente.|  
|%{Bucket Max}|Valore massimo dei membri da assegnare al gruppo di membri corrente.|  
|%{Previous Bucket Max}|Valore massimo dei membri da assegnare al gruppo di membri precedente.|  
|%{Next Bucket Min}|Valore minimo dei membri da assegnare al gruppo di membri successivo.|  
  
 Il modello di denominazione predefinito è `"%{First bucket member} - %{Last bucket member}"`, allo scopo di garantire la compatibilità con le versioni precedenti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
> [!NOTE]  
>  Per includere un punto e virgola (;) come carattere letterale nel modello di denominazione, utilizzare il simbolo di percentuale (%) come prefisso.  
  
### <a name="example"></a>Esempio  
 L'espressione stringa seguente può essere usata per classificare l'attributo Yearly Income della dimensione Customer del database di esempio [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , in cui per l'attributo Yearly Income viene usato il raggruppamento dei membri:  
  
 "Less than %{Next Bucket Min};Between %{First bucket member} and %{Last bucket member};Greater than %{Previous Bucket Max}"  
  
## <a name="adding-new-members-to-existing-member-groups"></a>Aggiunta di nuovi membri a gruppi di membri esistenti  
 I nuovi membri aggiunti alla dimensione vengono assegnati ai gruppi di membri appropriati confrontando il valore del membro con il layout di gruppi di membri corrente.  
  
 Se un membro viene inserito tra l'ultimo membro del gruppo di membri precedente e il primo membro del gruppo di membri successivo, il nuovo membro diventa l'ultimo membro del gruppo di membri precedente.  
  
## <a name="updating-a-dimension-with-discretized-attributes"></a>Aggiornamento di una dimensione con attributi discretizzati  
 Durante l'elaborazione di una dimensione, un attributo discretizzato verrà discretizzato di nuovo solo se si esegue un aggiornamento completo (ProcessFull). Per discretizzare di nuovo un attributo, è necessario eseguire un aggiornamento completo della dimensione. Se la tabella della dimensione di un attributo discretizzato viene aggiornata e la dimensione viene elaborata con un aggiornamento incrementale (ProcessAdd), l'attributo discretizzato non verrà discretizzato di nuovo. I nomi e gli elementi figlio dei nuovi bucket rimarranno invariati. Per altre informazioni sull'elaborazione delle dimensioni, vedere [Elaborazione di oggetti di Analysis Services](processing-analysis-services-objects.md).  
  
## <a name="usage-limitations"></a>Limitazioni all'utilizzo  
  
-   Non è possibile creare gruppi di membri nel livello più elevato o più basso di una gerarchia. Se tuttavia è necessario eseguire questa operazione, è possibile aggiungere un livello in modo tale che il livello in cui si desidera creare gruppi di membri non costituisca più il livello superiore o inferiore. Il livello aggiunto può essere nascosto impostandone la proprietà `Visible` su `False`.  
  
-   Non è possibile creare gruppi di membri in due livelli consecutivi di una gerarchia.  
  
-   Non sono supportati gruppi di membri per le dimensioni che utilizzano la modalità di archiviazione ROLAP.  
  
-   Se la tabella di una dimensione contenente gruppi di membri viene aggiornata e la dimensione viene quindi completamente elaborata, verrà generato un nuovo set di gruppi di membri. I nomi e gli elementi figlio dei nuovi gruppi di membri potranno essere diversi da quelli dei gruppi di membri precedenti.  
  
## <a name="see-also"></a>Vedere anche  
 [Attributi e gerarchie di attributi](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)  
  
  
