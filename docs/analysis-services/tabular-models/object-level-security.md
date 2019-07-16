---
title: Sicurezza a livello di oggetto del modello tabulare di Analysis Services | Microsoft Docs
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: d354aa64e8b6a1e98941011c30550a056f4c01c9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68162786"
---
# <a name="object-level-security"></a>Sicurezza a livello di oggetto
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
Protezione del modello di dati inizia con l'implementazione efficace [ruoli](../../analysis-services/tabular-models/roles-ssas-tabular.md) e i filtri a livello di riga per definire le autorizzazioni utente sui dati e oggetti modello di dati. A partire da modelli tabulari 1400, è anche possibile definire la sicurezza a livello di oggetto, che include la sicurezza a livello di tabella e la sicurezza a livello di colonna nel [oggetto Roles](https://docs.microsoft.com/bi-reference/tmsl/roles-object-tmsl).

## <a name="table-level-security"></a>Sicurezza a livello di tabella

Con la sicurezza a livello di tabella, non è possibile solo limitare l'accesso ai dati della tabella, ma anche i nomi di tabella sensibili, consentono di impedire agli utenti malintenzionati di individuare se una tabella esistente. 

 Sicurezza a livello di tabella è impostato nei metadati basati su JSON in Model. bim, [TMSL Tabular Model Scripting Language ()](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference), o [modello a oggetti tabulare (TOM)](https://docs.microsoft.com/bi-reference/tom/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo). Impostare il **metadataPermission** proprietà del **gli oggetti Tablepermission** classe la [oggetto Roles](https://docs.microsoft.com/bi-reference/tmsl/roles-object-tmsl) a **none**.

In questo esempio, la proprietà metadataPermission della classe gli oggetti Tablepermission per la tabella Product è impostata su none:

```
"roles": [
  {
    "name": "Users",
    "description": "All allowed users to query the model",
    "modelPermission": "read",
    "tablePermissions": [
      {
        "name": "Product",
        "metadataPermission": "none"
      }
    ]
  }
```

## <a name="column-level-security"></a>Sicurezza a livello di colonna

Simile alla sicurezza a livello di tabella, con sicurezza a livello di colonna è possibile non solo limitare l'accesso dati della colonna, ma anche i nomi delle colonne sensibili, consentono di impedire agli utenti malintenzionati di individuare una colonna.

 Sicurezza a livello di colonna è impostato nei metadati basati su JSON in Model. bim, [TMSL Tabular Model Scripting Language ()](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference), o [modello a oggetti tabulare (TOM)](https://docs.microsoft.com/bi-reference/tom/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo). Impostare il **metadataPermission** proprietà del **autorizzazioni per colonne** classe la [oggetto Roles](https://docs.microsoft.com/bi-reference/tmsl/roles-object-tmsl) a **none**.

In questo esempio, la proprietà metadataPermission della classe di autorizzazioni per colonne per la colonna tariffa di Base nella tabella Employees è impostata su none:

```
"roles": [
  {
    "name": "Users",
    "description": "All allowed users to query the model",
    "modelPermission": "read",
    "tablePermissions": [
      {
        "name": "Employee",
        "columnPermissions": [
          {
            "name": "Base Rate",
            "metadataPermission": "none"
          }
        ]
      }
    ]
  }
```

## <a name="restrictions"></a>Restrizioni

*  Sicurezza a livello di tabella non può essere impostata per un modello se interrompe una catena di relazioni. Viene generato un errore in fase di progettazione.
 Se sono presenti relazioni tra le tabelle A e B e B e C, ad esempio, non è possibile proteggere tabella B. Se nella tabella B è protetto, una query sulla tabella non può passare le relazioni tra la tabella A e B e B e C. In questo caso, è stato possibile configurare una relazione separata tra le tabelle A e B.

    ![Sicurezza a livello di tabella](../../analysis-services/tabular-models/media/ssas-ols.png)  


*  Sicurezza a livello di riga e la sicurezza a livello di oggetto nelze kombinovat dai diversi ruoli perché potrebbe introdurre accesso non autorizzato ai dati protetti. Viene generato un errore in fase di query per gli utenti che sono membri di questo tipo una combinazione di ruoli.

*  Calcoli dinamici (misure, indicatori KPI, DetailRows) sono automaticamente limitati che fanno riferimento a una tabella protetta o una colonna. Anche se non esiste alcun meccanismo per proteggere in modo esplicito una misura, è possibile proteggere in modo implicito una misura, aggiornando l'espressione per fare riferimento a una tabella protetta o una colonna.

*  Le relazioni che fanno riferimento a una colonna protetta di lavoro fornito non è protetto nella tabella che la colonna è inclusa.




## <a name="see-also"></a>Vedere anche  
[Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
[Oggetto Roles (TMSL)](https://docs.microsoft.com/bi-reference/tmsl/roles-object-tmsl)  
[Supporto per TMSL (Tabular Model Scripting Language) in SSMS](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference)  
[Modello a oggetti tabulare (TOM)](https://docs.microsoft.com/bi-reference/tom/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo).

  
