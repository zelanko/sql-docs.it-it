---
title: Definisci funzioni semiadditive | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1ab36e1835af05010fa3fa206e49feec6161c31d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68178638"
---
# <a name="define-semiadditive-behavior"></a>Definire una funzione semiadditiva
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Le misure semiadditive, che non aggregano in modo uniforme di tutte le dimensioni, sono molto comuni in numerosi scenari aziendali. Ogni cubo basato su snapshot di saldi nel tempo sono caratterizzati da questo problema. Questi snapshot si trovano in applicazioni per la gestione di titoli, saldi contabili, budget, risorse umane, polizze e risarcimenti assicurativi e numerosi altri scenari aziendali.  
  
 L'aggiunta di funzioni semiadditive a un cubo consente di definire un metodo di aggregazione per singole misure o singoli membri dell'attributo del tipo Conto. Se il cubo contiene una dimensione di tipo Conti, è possibile impostare automaticamente le funzioni semiadditive in base al tipo di conto.  
  
 Per aggiungere funzioni semiadditive aprire un cubo in Progettazione cubi e scegliere **Aggiungi funzionalità di Business Intelligence** dal menu Cubo. Nella Configurazione guidata funzionalità di Business Intelligence selezionare l'opzione **Definizione funzioni semiadditive** nella pagina **Scelta funzionalità avanzata** . Questa procedura guidata consente di eseguire in modo semplificato i passaggi necessari per definire le misure contenenti funzioni semiadditive.  
  
 Ad eccezione di LastChild disponibile nell'edizione Standard, le funzioni semiadditive sono disponibili solo in Business Intelligence o nelle edizioni Enterprise.  
  
## <a name="define-semiadditive-behavior"></a>Definire una funzione semiadditiva  
 Nella pagina **Definizione funzioni semiadditive** della procedura guidata selezionare la modalità di definizione delle funzioni semiadditive selezionando una delle opzioni seguenti:  
  
 **Disabilita funzioni semiadditive**  
 Consente di rimuovere le funzioni semiadditive da un cubo in cui tali funzioni sono state precedentemente definite. Se si seleziona questa opzione, una misura viene reimpostata su **SUM** se è impostata su uno dei tipi di funzione di aggregazione seguenti:  
  
-   By Account  
  
-   Average of Children  
  
-   First Child  
  
-   Last Child  
  
-   Last Nonempty Child  
  
-   First Nonempty Child  
  
-   Nessuna  
  
 Questa opzione non modifica le misure con una funzione di aggregazione regolare: **Somma**, **Min**, **Max**, **conteggio**, o **Distinct * * * conteggio**.  
  
 **La procedura guidata ha rilevato il ' Account "dimensione di tipo conti, che contiene membri semiadditivi. Il server aggregherà i membri di questa dimensione in base alle funzioni semiadditive specificate per ogni tipo di account.**  
 Tutte le misure di un gruppo di misure dimensionate in base a una dimensione di tipo Conti verranno impostate dal sistema sulla funzione di aggregazione By Account e i membri della dimensione verranno aggregati dal server in base alle funzioni semiadditive specificate per ogni tipo di conto.  
  
> [!NOTE]  
>  Questa opzione è selezionata per impostazione predefinita se la procedura guidata rileva una dimensione di tipo Conti.  
  
 **Definisci funzioni semiadditive per singole misure**  
 Consente di selezionare individualmente le funzioni semiadditive di ogni misura. L'impostazione predefinita è **SUM** (additività completa).  
  
> [!NOTE]  
>  Questa opzione è selezionata per impostazione predefinita se la procedura guidata non rileva una dimensione di tipo Conti.  
  
 Per ogni misura è possibile selezionare tra i tipi di funzionalità semiadditive descritti nella tabella seguente.  
  
|Funzione semiadditiva|Descrizione|  
|---------------------------|-----------------|  
|Average of Children|La funzione di aggregazione di un membro corrisponde alla media dei relativi figli.|  
|ByAccount|Il sistema legge le funzioni semiadditive specificate per il tipo di conto.|  
|Count|La funzione di aggregazione corrisponde a un conteggio dei membri.|  
|Distinct Count|La funzione di aggregazione corrisponde a un conteggio dei membri univoci.|  
|First Child|Il valore del membro viene valutato come il valore del relativo primo figlio assieme alla dimensione temporale.|  
|FirstNonEmpty|Il valore del membro viene valutato come il valore del relativo primo figlio assieme alla dimensione temporale contenente dati.|  
|LastChild|Il valore del membro viene valutato come il valore del relativo ultimo figlio assieme alla dimensione temporale.|  
|LastNonEmpty|Il valore del membro viene valutato come il valore del relativo ultimo figlio assieme alla dimensione temporale contenente dati.|  
|Max|Viene applicata la funzione di aggregazione massima standard.|  
|Min|Viene applicata la funzione di aggregazione minima standard.|  
|Nessuna|Non viene applicata alcuna funzione di aggregazione.|  
|SUM|Viene applicata la funzione di somma standard.|  
  
 Al termine della procedura guidata le funzioni semiadditive esistenti vengono sovrascritte.  
  
  
