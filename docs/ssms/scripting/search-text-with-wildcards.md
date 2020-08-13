---
title: Testo di ricerca con caratteri jolly
description: Informazioni su come usare i caratteri jolly nel campo "Trova" di una finestra di dialogo Trova e sostituisci per specificare un criterio per la corrispondenza.
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- vswildcardsbuilder
helpviewer_keywords:
- searches [SQL Server Management Studio], wildcards
- Query Editor [SQL Server Management Studio], wildcard searches
- wildcard options [SQL Server Management Studio]
ms.assetid: 449600f8-cc87-4b3f-878a-59c158a88a40
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c8e2766939038879d92de0f8f73b5c2eab38f45d
ms.sourcegitcommit: d855def79af642233cbc3c5909bc7dfe04c4aa23
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2020
ms.locfileid: "87122792"
---
# <a name="search-text-with-wildcards"></a>Testo di ricerca con caratteri jolly
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  Le espressioni seguenti possono sostituire caratteri o cifre nel campo **Trova** della finestra di dialogo **Trova e sostituisci** di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-search-using-wildcards"></a>Per eseguire la ricerca utilizzando caratteri jolly  
  
1.  Per consentire l'uso di caratteri jolly nel campo **Trova** durante operazioni Ricerca veloce, **Cerca nei file**, **Sostituzione veloce**o **Sostituisci nei file** , selezionare l'opzione **Utilizza** in **Opzioni di ricerca** e quindi scegliere **Caratteri jolly**.  
  
2.  Accanto al campo **Trova** viene reso disponibile il pulsante triangolare per **l'elenco dei riferimenti**. Fare clic su di esso per visualizzare l'elenco dei caratteri jolly disponibili. L'elemento scelto dall' **Elenco riferimenti**viene inserito nella stringa **Trova** .  
  
 Nella tabella seguente sono descritti i caratteri jolly disponibili nell' **Elenco riferimenti**.  
  
|Expression|Sintassi|Descrizione|  
|----------------|------------|-----------------|  
|Un solo carattere|?|Individua un qualsiasi singolo carattere.|  
|Una sola cifra|#|Individua una qualsiasi singola cifra. Ad esempio, 7# individua i numeri che comprendono 7 seguito da un altro numero. In questo caso potrebbe essere 71 ma non 17.|  
|Qualsiasi carattere esterno al set|[! ]|Individua qualsiasi carattere non specificato nel set.|  
|Zero o più caratteri|*|Individua uno o più caratteri. Ad esempio, nuovo* individua qualsiasi testo che comprende "nuovo", come nuovofile.txt.|  
|Qualsiasi carattere del set|[ ]|Individua qualsiasi carattere specificato nel set.|  
  
## <a name="see-also"></a>Vedere anche  
 [Ricerca e sostituzione](../../relational-databases/scripting/search-and-replace.md)   
 [Eseguire ricerche di testo con espressioni regolari](../../relational-databases/scripting/search-text-with-regular-expressions.md)  
