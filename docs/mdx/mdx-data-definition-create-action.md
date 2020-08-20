---
description: Definizione dei dati MDX - CREATE ACTION
title: Istruzione CREATE ACTION (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7132c28e93dbc11eee1c5a4e4d53126f280fa74a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494904"
---
# <a name="mdx-data-definition---create-action"></a>Definizione dei dati MDX - CREATE ACTION


  Crea un'azione che può essere associata a un cubo, a una dimensione, a una gerarchia o a un oggetto subordinato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
CREATE ACTION CURRENTCUBE | Cube_Name  
   .Action_Name <action body>  
<action body> ::=   
FOR   
        CUBE   
    | Hierarchy_Name [MEMBERS]   
    | Level_Name [MEMBERS]   
    | CELLS   
    | SET }   
      AS 'MDX_Expression'   
        [, TYPE = '  
              { URL   
            | HTML   
            | STATEMENT   
               | DATASET   
            | ROWSET   
            | COMMANDLINE   
               | PROPRIETARY }   
         ']  
   [ , INVOCATION = 'INTERACTIVE | ON_OPEN | BATCH ' ]  
   [ , APPLICATION = String_Expression ]  
   [ , DESCRIPTION = String_Expression ]  
   [ , CAPTION = 'MDX_Expression' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 *Cube_Name*  
 Stringa valida che specifica il nome di un cubo.  
  
 *Nome Action_*  
 Stringa valida che specifica il nome dell'azione da creare.  
  
 *Nome Hierarchy_*  
 Stringa valida che specifica il nome di una gerarchia.  
  
 *Nome Level_*  
 Stringa valida che specifica il nome di un livello.  
  
 *Nome Member_*  
 Stringa valida che specifica il nome o la chiave di un membro.  
  
 *MDX_Expression*  
 Espressione MDX valida.  
  
 *String_Expression*  
 Espressione stringa valida.  
  
## <a name="remarks"></a>Osservazioni  
 Le applicazioni client possono creare ed eseguire azioni non sicure, così come possono utilizzare funzioni non sicure. Per evitare queste situazioni, utilizzare la proprietà **Opzioni di sicurezza** . Per ulteriori informazioni, vedere l'argomento dedicato alle opzioni di sicurezza.  
  
> [!NOTE]  
>  Questa istruzione è stata inclusa per compatibilità con le versioni precedenti. Le azioni nuove a [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , ad esempio le azioni drill-through o report, non sono supportate.  
  
## <a name="action-types"></a>Tipi di azioni  
 Nella tabella seguente vengono descritti i diversi tipi di azioni disponibili in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
|Tipo di azione|Descrizione|  
|-----------------|-----------------|  
|**URL**|Viene restituita una stringa costituita da un URL a cui accedere tramite browser Internet.<br /><br /> Nota: se questa azione non inizia con `https://` o `https://` , l'azione non sarà disponibile per il browser, a meno che **SafetyOptions** non sia impostato su **DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_ALL**.|  
|**HTML**|Viene restituita una stringa costituita da uno script HTML. Tale stringa deve essere salvata in un file che sarà possibile visualizzare utilizzando un browser Internet. In questo caso è possibile che nell'ambito del codice HTML generato venga eseguito un intero script.|  
|**ISTRUZIONE**|La stringa di azione restituita è un'istruzione che deve essere eseguita impostando il metodo **ICommand:: SetText** di un oggetto Command sulla stringa e chiamando il metodo **ICommand:: Execute**. Se il comando non riesce, verrà restituito un errore.|  
|**DATASET**|La stringa di azione restituita è un'istruzione MDX che deve essere eseguita impostando il metodo **ICommand:: SetText** di un oggetto Command sulla stringa e chiamando il metodo **ICommand:: Execute** . L'ID di interfaccia richiesto (IID) dovrebbe essere **IDataset**. Il comando riesce se viene creato un set di dati. L'applicazione client deve consentire all'utente di visualizzare il set di dati restituito.|  
|**RIGHE**|Analogamente al **set di dati**, ma anziché richiedere un IID di **IDataset**, l'applicazione client deve richiedere un IID di **IRowset**. Il comando riesce se viene creato un set di righe. L'applicazione client deve consentire all'utente di visualizzare il set di righe restituito.|  
|**COMMANDLINE**|L'applicazione client deve eseguire la stringa dell'azione, che è costituita da una riga di comando.|  
|**PROPRIETARIO**|L'applicazione client può visualizzare o eseguire l'azione esclusivamente se dispone di informazioni personalizzate, non generiche, sull'azione specifica. Le azioni proprietarie non vengono restituite all'applicazione client a meno che l'applicazione client non le chieda esplicitamente impostando la restrizione appropriata per la **application_name**.|  
  
## <a name="invocation-types"></a>Tipi di chiamate  
 Nella tabella seguente vengono descritti i diversi tipi di chiamate disponibili in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Il tipo di chiamata viene utilizzato dall'applicazione client solo per determinare quando richiamare l'azione, ma non determina effettivamente il comportamento di chiamata dell'azione.  
  
|Tipo di chiamata|Descrizione|  
|---------------------|-----------------|  
|**INTERATTIVA**|L'azione deve essere richiamata dall'applicazione client tramite l'interazione dell'utente.|  
|**ON_OPEN**|L'azione deve essere richiamata dall'applicazione client quando viene aperto l'oggetto di destinazione. Questo tipo di chiamata non è attualmente implementato.|  
|**BATCH**|L'azione deve essere richiamata dall'applicazione client quando l'oggetto di destinazione è coinvolto in un'operazione batch, secondo quanto determinato dall'applicazione client. Questo tipo di chiamata non è attualmente implementato.|  
  
### <a name="scope"></a>Scope  
 Ogni azione è definita per un cubo specifico e ha un nome univoco in tale cubo. Un'azione può avere uno degli ambiti elencati nella tabella seguente.  
  
 Ambito cubo  
 Per azioni indipendenti da una dimensione, una cella o un membro specifico, ad esempio l'avvio di un'emulazione di terminale per un sistema di produzione AS/400.  
  
 Ambito dimensione  
 L'azione viene applicata a una dimensione specifica. Le azioni di questo tipo non dipendono dagli specifici livelli o membri selezionati.  
  
 Ambito livello  
 L'azione viene applicata a un livello di dimensione specifico. Le azioni di questo tipo non dipendono dallo specifico membro selezionato nella dimensione.  
  
 Ambito membro  
 L'azione viene applicata a membri specifici di un livello.  
  
 Ambito cella  
 L'azione viene applicata solo a celle specifiche.  
  
 Ambito set  
 L'azione viene applicata solo a un set. Il nome, **ActionParameterSet**, è riservato per l'utilizzo da parte dell'applicazione all'interno dell'espressione dell'azione.  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzioni MDX per la definizione dei dati &#40;&#41;MDX ](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
