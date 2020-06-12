---
title: Definire calcoli della funzionalità di Business Intelligence per l'ora mediante configurazione guidata funzionalità di Business Intelligence Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- period over period growth [Analysis Services]
- parallel period comparisons [Analysis Services]
- Business Intelligence enhancements [Analysis Services], time intelligence
- time views [Analysis Services]
- hierarchies [Analysis Services], time
- time periods [Analysis Services]
- moving averages
- time [Analysis Services]
- period to date [Analysis Services]
- calculations [Analysis Services], time
- time hierarchies [Analysis Services]
- time intelligence [Analysis Services]
ms.assetid: be36e8fc-f46e-4553-8623-b27d695c330b
author: minewiskan
ms.author: owend
ms.openlocfilehash: 8c0ebb99e8368254e085cc9a4f4b0dc9a040b24c
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546958"
---
# <a name="define-time-intelligence-calculations-using-the-business-intelligence-wizard"></a>Definire calcoli delle funzionalità di Business Intelligence per le gerarchie temporali mediante la Configurazione guidata funzionalità di Business Intelligence
  La funzionalità avanzata di Business Intelligence per le gerarchie temporali corrisponde alla funzionalità avanzata a livello di cubo basata sull'aggiunta di calcoli temporali o viste temporali a una gerarchia selezionata. Questa funzionalità avanzata supporta le categorie di calcolo seguenti:  
  
-   Da inizio periodo fino alla data specificata.  
  
-   Incremento rispetto al periodo precedente.  
  
-   Medie mobili.  
  
-   Confronti di periodi paralleli.  
  
 È possibile applicare la funzionalità di Business Intelligence per le gerarchie temporali a cubi che dispongono di una dimensione temporale, ovvero una dimensione la cui proprietà `Type` è impostata su `Time`. Gli attributi temporali di tale dimensione devono inoltre disporre di impostazioni adeguate, ad esempio Anni o Mesi, per la corrispondente proprietà `Type`. La proprietà `Type` della dimensione e dei relativi attributi verrà impostata correttamente se per la creazione della dimensione temporale si utilizza Creazione guidata dimensione.  
  
 Per aggiungere funzionalità di Business Intelligence per le gerarchie temporali a un cubo, è possibile usare la Configurazione guidata funzionalità di Business Intelligence, quindi selezionare l'opzione **Definizione funzionalità di Business Intelligence per le gerarchie temporali** nella pagina **Scelta funzionalità avanzata** . Questa procedura guidata consente di eseguire in modo semplificato la selezione di una gerarchia a cui aggiungere la funzionalità di Business Intelligence per le gerarchie temporali e la definizione dei membri della gerarchia ai quali verrà applicata la funzionalità di Business Intelligence per le gerarchie temporali. Nell'ultima pagina della procedura guidata è possibile visualizzare le modifiche che verranno apportate al [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database per aggiungere la funzionalità di Business Intelligence per l'ora selezionata.  
  
## <a name="selecting-a-time-hierarchy"></a>Selezione di una gerarchia temporale  
 Nella pagina **Scelta calcoli e gerarchia di destinazione** selezionare la gerarchia temporale a cui si desidera applicare la funzionalità avanzata. Questa funzionalità avanzata può essere applicata solo a una gerarchia temporale durante l'esecuzione di Configurazione guidata funzionalità di Business Intelligence. Se si desidera applicare la funzionalità avanzata a più gerarchie temporali, è necessario eseguire nuovamente la procedura guidata.  
  
 Dopo aver selezionato una gerarchia temporale, nell'elenco **Calcoli temporali disponibili** selezionare i calcoli da applicare alla gerarchia. I calcoli disponibili dipendono dai livelli inclusi nella gerarchia e dalle impostazioni della proprietà `Type` per l'attributo di ogni livello. Ad esempio, una gerarchia Anni supporta Da inizio anno e Incremento rispetto all'anno precedente, a differenza di una gerarchia Trimestri.  
  
> [!NOTE]  
>  Il file modello Timeintelligence.xml definisce i calcoli temporali visualizzati in **Calcoli temporali disponibili**. Se i calcoli disponibili non soddisfano le specifiche esigenze, è possibile modificare i calcoli esistenti oppure aggiungerne di nuovi al file Timeintelligence.xml.  
  
> [!TIP]  
>  Per visualizzare la descrizione di un calcolo, utilizzare i tasti freccia SU e GIÙ per evidenziare il calcolo desiderato.  
  
## <a name="apply-time-views-to-members"></a>Applicazione di viste temporali ai membri  
 Nella pagina **Definizione ambito dei calcoli** specificare i membri ai quali si desidera applicare nuove viste temporali. È possibile applicare nuove viste temporali a uno degli oggetti seguenti:  
  
-   **Membri di una dimensione di tipo Conti** Nella pagina **Definizione ambito dei calcoli** l'elenco **Misure disponibili** include le dimensioni di tipo Conti, ovvero dimensioni la cui proprietà `Type` è impostata su `Accounts`. Se si dispone di una dimensione di tipo Conti, ma tale dimensione non è visualizzata nell'elenco **Misure disponibili** , è possibile usare Configurazione guidata funzionalità di Business Intelligence per applicare la funzionalità di Business Intelligence per la contabilità a tale dimensione. Per altre informazioni, vedere [Aggiungere funzionalità di Business Intelligence per la contabilità a una dimensione](bi-wizard-add-account-intelligence-to-a-dimension.md).  
  
-   **Misure** Anziché specificare una dimensione di tipo Conti è possibile specificare le misure alle quali applicare le viste temporali. In questo caso, selezionare le viste alle quali applicare i calcoli temporali selezionati. Ad esempio, le attività e passività includono dati di tipo Da inizio anno. Pertanto non verrà applicato un calcolo Da inizio anno alle misure relative ad attività e passività.  
  
## <a name="viewing-the-time-intelligence-enhancement"></a>Visualizzazione dei miglioramenti della funzionalità di Business Intelligence per le gerarchie temporali  
 Nell'ultima pagina di Configurazione guidata funzionalità di Business Intelligence è possibile visualizzare le modifiche che verranno apportate al database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Nel caso di funzionalità avanzate di Business Intelligence per le gerarchie temporali, la procedura guidata modificherà la dimensione temporale selezionata, la vista origine dati associata e il cubo associato come illustrato nella tabella seguente.  
  
|Oggetto|Modifica|  
|------------|------------|  
|Dimensione temporale|Aggiunta di un attributo per ogni calcolo o vista.|  
|Vista origine dati|Aggiunta di una colonna calcolata nella tabella dei tempi per ogni nuovo attributo nella dimensione temporale.|  
|Cube|Aggiunta di un membro calcolato che definisce il codice MDX (Multidimensional Expressions) per l'esecuzione del calcolo.|  
  
## <a name="see-also"></a>Vedere anche  
 [Creare membri calcolati](create-calculated-members.md)  
  
  
