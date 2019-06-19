---
title: Aggiungere funzionalità di Business Intelligence a una dimensione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], Business Intelligence enhancements
- Business Intelligence enhancements [Analysis Services], account intelligence
- account intelligence [Analysis Services]
ms.assetid: 36f454ae-a9f2-4a59-b19d-40310af9f901
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 111948911c0fe7bdc0e7ce260a15b8efee50e9db
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66076895"
---
# <a name="add-account-intelligence-to-a-dimension"></a>Aggiungere funzionalità di Business Intelligence per la contabilità a una dimensione
  È possibile aggiungere la funzionalità di Business Intelligence per la contabilità a un cubo o una dimensione per assegnare classificazioni standard, ad esempio entrate e uscite, ai membri di un attributo di tipo Conto. Questa funzionalità consente inoltre di identificare i tipi di conto, ad esempio Asset e Liability, e di assegnare l'aggregazione appropriata a ogni tipo di conto. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] può usare le classificazioni per aggregare i conti nel tempo.  
  
> [!NOTE]  
>  La funzionalità di Business Intelligence per la contabilità è disponibile solo per le dimensioni basate su origini dei dati esistenti. Per le dimensioni create senza utilizzare un'origine dei dati, prima di aggiungere questa funzionalità è necessario eseguire la Generazione guidata schema per creare una vista origine dati.  
  
 La funzionalità di Business Intelligence per la contabilità viene applicata a una dimensione contenente informazioni sui conti, ad esempio il nome, il numero e il tipo del conto. Per aggiungere questa funzionalità, usare la Configurazione guidata funzionalità di Business Intelligence e selezionare l'opzione **Funzionalità di Business Intelligence per la contabilità** nella pagina **Scelta funzionalità avanzata** . Questa procedura guidata consente di eseguire in modo semplificato i passaggi necessari per selezionare una dimensione a cui si desidera applicare la funzionalità di Business Intelligence per la contabilità, identificare gli attributi Conto nella dimensione di tipo Conti selezionata e quindi eseguire il mapping dei tipi di conto nella tabella della dimensione ai tipi di conto riconosciuti da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="selecting-a-dimension"></a>Selezione di una dimensione  
 Nella prima pagina **Funzionalità di Business Intelligence per la contabilità** della procedura guidata specificare la dimensione a cui si vuole applicare questa funzionalità. L'aggiunta della funzionalità di Business Intelligence per la contabilità alla dimensione selezionata comporterà modifiche della dimensione. Tali modifiche verranno ereditate da tutti i cubi che includono la dimensione selezionata.  
  
## <a name="specifying-account-attributes"></a>Impostazione degli attributi Conto  
 Nella pagina **Configurazione attributi dimensione** della procedura guidata specificare gli attributi Conto nella dimensione di tipo Conti selezionata. Selezionare innanzitutto nella colonna **Includi** la casella di controllo accanto a ogni tipo di attributo Conto di cui si vuole eseguire il mapping a un attributo nella dimensione. Espandere quindi l'elenco a discesa nella colonna **Attributo dimensione** e selezionare l'attributo nella dimensione corrispondente al tipo di attributo selezionato. Quando si seleziona l'attributo da questo elenco, viene impostata la proprietà `Type` degli attributi Conto.  
  
## <a name="mapping-account-types"></a>Mapping dei tipi di conto  
 La seconda pagina **Funzionalità di Business Intelligence per la contabilità** consente di eseguire il mapping dei tipi di conto nella tabella della dimensione ai tipi di conto riconosciuti da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Questa pagina viene visualizzata solo se nella dimensione è stato aggiunto l'attributo **Tipo conto** . Per includere la dimensione **Tipo conto** , nella pagina **Funzionalità di Business Intelligence per la contabilità** della procedura guidata selezionare la casella di controllo accanto a **Tipo conto**e quindi selezionare l'attributo appropriato.  
  
 Nella seconda pagina **Funzionalità di Business Intelligence per la contabilità** sono disponibili due colonne:  
  
-   Nella colonna **Tipi di conto tabella di origine** sono elencati i tipi di conto recuperati dalla tabella della dimensione.  
  
-   Nella colonna **Tipi di conto del server** è identificato il tipo di conto corrispondente riconosciuto da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . La tabella seguente elenca i tipi di conto riconosciuti da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e l'aggregazione predefinita per ognuno di essi. Se nella tabella della dimensione vengono usati gli stessi nomi dei tipi di conto riconosciuti da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , queste selezioni vengono eseguite automaticamente.  
  
    |Tipo di conto del server|Aggregazione|Descrizione|  
    |-------------------------|-----------------|-----------------|  
    |**Statistiche**|`None`|Rapporto calcolato oppure conteggio che non viene aggregato nel tempo. Questo tipo di conto non viene convertito da una valuta all'altra in base alle regole di conversione.|  
    |**Liability**|`LastNonEmpty`|Importo di denaro o valore dei beni di cui si è debitori in un dato momento. Questo tipo di conto non cresce e quindi non viene aggregato in modo naturale nel tempo. Ad esempio, l'importo relativo all'anno è il valore dell'ultimo mese con i dati. Questo tipo di conto viene convertito da una valuta all'altra in base al tasso di fine periodo.|  
    |**Asset**|`LastNonEmpty`|Importo di denaro o valore dei beni di cui si è in possesso in un dato momento. Questo tipo di conto cresce e quindi non viene aggregato in modo naturale nel tempo. Ad esempio, l'importo relativo all'anno è il valore dell'ultimo mese con i dati. Questo tipo di conto viene convertito da una valuta all'altra in base al tasso di fine periodo.|  
    |**Balance**|`LastNonEmpty`|Conteggio risultante in un dato momento. Questo tipo di conto cresce, ma non viene aggregato in modo naturale nel tempo. Ad esempio, l'importo relativo all'anno è il valore dell'ultimo mese con i dati.|  
    |**Flow**|`Sum`|Conteggio incrementale. Questo tipo di conto viene aggregato in base alla funzione `Sum` nel tempo, ma non viene convertito in base alle regole di conversione della valuta.|  
    |**Expense**|`Sum`|Importo di denaro o valore dei beni speso. Questo tipo di conto viene aggregato in base alla funzione `Sum` nel tempo e viene convertito da una valuta all'altra in base a un tasso medio.|  
    |**Income**|`Sum`|Importo di denaro o valore dei beni ricevuto. Questo tipo di conto viene aggregato in base alla funzione `Sum` nel tempo e viene convertito da una valuta all'altra in base a un tasso medio.|  
  
    > [!NOTE]  
    >  Se appropriato, è possibile eseguire il mapping di più tipi di conto nella dimensione a un tipo di conto del server specifico.  
  
 Per modificare le aggregazioni predefinite di cui è stato eseguito il mapping a ogni tipo di conto per un database, è possibile utilizzare Progettazione database.  
  
1.  In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto di Analysis Services e scegliere **Modifica database**.  
  
2.  Nella casella **Mapping tipi di conto** selezionare un tipo in **Nome**.  
  
3.  Nella casella di testo **Alias** digitare un alias per il tipo di conto.  
  
4.  Nell'elenco a discesa **Funzione di aggregazione** modificare la funzione di aggregazione predefinita per il tipo di conto.  
  
  
