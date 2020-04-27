---
title: Definire il comportamento di funzioni semiadditive | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- semiadditive
- Business Intelligence enhancements [Analysis Services], semiadditive behavior
- measures [Analysis Services], semiadditive
ms.assetid: b25726bc-728b-4601-ad87-9015c39dc615
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c72cc6b3798d790b4787cb5fcfe3e560b6580fc2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66075543"
---
# <a name="define-semiadditive-behavior"></a>Definire una funzione semiadditiva
  Le misure semiadditive, che non aggregano in modo uniforme di tutte le dimensioni, sono molto comuni in numerosi scenari aziendali. Ogni cubo basato su snapshot di saldi nel tempo sono caratterizzati da questo problema. Questi snapshot si trovano in applicazioni per la gestione di titoli, saldi contabili, budget, risorse umane, polizze e risarcimenti assicurativi e numerosi altri scenari aziendali.  
  
 L'aggiunta di funzioni semiadditive a un cubo consente di definire un metodo di aggregazione per singole misure o singoli membri dell'attributo del tipo Conto. Se il cubo contiene una dimensione di tipo Conti, è possibile impostare automaticamente le funzioni semiadditive in base al tipo di conto.  
  
 Per aggiungere funzioni semiadditive aprire un cubo in Progettazione cubi e scegliere **Aggiungi funzionalità di Business Intelligence** dal menu Cubo. Nella Configurazione guidata funzionalità di Business Intelligence selezionare l'opzione **Definizione funzioni semiadditive** nella pagina **Scelta funzionalità avanzata** . Questa procedura guidata consente di eseguire in modo semplificato i passaggi necessari per definire le misure contenenti funzioni semiadditive.  
  
 Ad eccezione di LastChild disponibile nell'edizione Standard, le funzioni semiadditive sono disponibili solo in Business Intelligence o nelle edizioni Enterprise.  
  
## <a name="define-semiadditive-behavior"></a>Definire una funzione semiadditiva  
 Nella pagina **Definizione funzioni semiadditive** della procedura guidata selezionare la modalità di definizione delle funzioni semiadditive selezionando una delle opzioni seguenti:  
  
 **Disabilita funzioni semiadditive**  
 Consente di rimuovere le funzioni semiadditive da un cubo in cui tali funzioni sono state precedentemente definite. Se si seleziona questa opzione, una misura viene reimpostata su `SUM` se è impostata su uno dei tipi di funzione di aggregazione seguenti:  
  
-   By Account  
  
-   Average of Children  
  
-   First Child  
  
-   Last Child  
  
-   Last Nonempty Child  
  
-   First Nonempty Child  
  
-   nessuno  
  
 Questa opzione non modifica le misure con una funzione di aggregazione `Sum`regolare `Min`: `Max`, `Count`,, `Distinct``Count`o.  
  
 **La procedura guidata ha rilevato la dimensione di tipo Conti ' account ', che contiene membri funzioni semiadditive. Il server aggrega i membri di questa dimensione in base al comportamento funzioni semiadditive specificato per ogni tipo di conto.**  
 Tutte le misure di un gruppo di misure dimensionate in base a una dimensione di tipo Conti verranno impostate dal sistema sulla funzione di aggregazione By Account e i membri della dimensione verranno aggregati dal server in base alle funzioni semiadditive specificate per ogni tipo di conto.  
  
> [!NOTE]  
>  Questa opzione è selezionata per impostazione predefinita se la procedura guidata rileva una dimensione di tipo Conti.  
  
 **Definisci funzioni semiadditive per singole misure**  
 Consente di selezionare individualmente le funzioni semiadditive di ogni misura. L'impostazione predefinita è `SUM` (additività completa).  
  
> [!NOTE]  
>  Questa opzione è selezionata per impostazione predefinita se la procedura guidata non rileva una dimensione di tipo Conti.  
  
 Per ogni misura è possibile selezionare tra i tipi di funzionalità semiadditive descritti nella tabella seguente.  
  
|Funzione semiadditiva|Descrizione|  
|---------------------------|-----------------|  
|Average of Children|La funzione di aggregazione di un membro corrisponde alla media dei relativi figli.|  
|ByAccount|Il sistema legge le funzioni semiadditive specificate per il tipo di conto.|  
|Conteggio|La funzione di aggregazione corrisponde a un conteggio dei membri.|  
|Distinct Count|La funzione di aggregazione corrisponde a un conteggio dei membri univoci.|  
|First Child|Il valore del membro viene valutato come il valore del relativo primo figlio assieme alla dimensione temporale.|  
|FirstNonEmpty|Il valore del membro viene valutato come il valore del relativo primo figlio assieme alla dimensione temporale contenente dati.|  
|LastChild|Il valore del membro viene valutato come il valore del relativo ultimo figlio assieme alla dimensione temporale.|  
|LastNonEmpty|Il valore del membro viene valutato come il valore del relativo ultimo figlio assieme alla dimensione temporale contenente dati.|  
|Max|Viene applicata la funzione di aggregazione massima standard.|  
|Min|Viene applicata la funzione di aggregazione minima standard.|  
|nessuno|Non viene applicata alcuna funzione di aggregazione.|  
|SUM|Viene applicata la funzione di somma standard.|  
  
 Al termine della procedura guidata le funzioni semiadditive esistenti vengono sovrascritte.  
  
  
