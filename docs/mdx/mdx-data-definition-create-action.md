---
title: Istruzione CREATE ACTION (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b723a706521b24c9aa216c46f617d8ff94997137
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68098550"
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
  
## <a name="remarks"></a>Note  
 Le applicazioni client possono creare ed eseguire azioni non sicure, così come possono utilizzare funzioni non sicure. Per evitare queste situazioni, usare il **opzioni di sicurezza** proprietà. Per ulteriori informazioni, vedere l'argomento dedicato alle opzioni di sicurezza.  
  
> [!NOTE]  
>  Questa istruzione è stata inclusa per compatibilità con le versioni precedenti. Familiarità con le azioni [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], ad esempio le azioni di drill-through o Report, non sono supportati.  
  
## <a name="action-types"></a>Tipi di azioni  
 La tabella seguente descrive i diversi tipi di azioni disponibili in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
|Tipo di azione|Descrizione|  
|-----------------|-----------------|  
|**URL**|Viene restituita una stringa costituita da un URL a cui accedere tramite browser Internet.<br /><br /> Nota: Se questa azione non inizia con `https://` oppure `https://`, l'azione sarà disponibile al browser, a meno che **SafetyOptions** è impostata su **DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_ALL**.|  
|**HTML**|Viene restituita una stringa costituita da uno script HTML. Tale stringa deve essere salvata in un file che sarà possibile visualizzare utilizzando un browser Internet. In questo caso è possibile che nell'ambito del codice HTML generato venga eseguito un intero script.|  
|**ISTRUZIONE**|La stringa restituita è un'istruzione che deve essere eseguito impostando il **SetText** metodo di un oggetto comando per la stringa e la chiamata il **ICommand:: Execute**(metodo). Se il comando non riesce, verrà restituito un errore.|  
|**DATASET**|La stringa restituita è un'istruzione MDX che deve essere eseguita impostando il **SetText** metodo di un oggetto comando per la stringa e la chiamata il **ICommand:: Execute** (metodo). L'interfaccia richiesta ID (IID) deve essere **IDataset**. Il comando riesce se viene creato un set di dati. L'applicazione client deve consentire all'utente di visualizzare il set di dati restituito.|  
|**SET DI RIGHE**|Simile a **set di dati**, ma anziché richiedere un IID di **IDataset**, l'applicazione client deve richiedere un IID di **IRowset**. Il comando riesce se viene creato un set di righe. L'applicazione client deve consentire all'utente di visualizzare il set di righe restituito.|  
|**RIGA DI COMANDO**|L'applicazione client deve eseguire la stringa dell'azione, che è costituita da una riga di comando.|  
|**PROPRIETARY**|L'applicazione client può visualizzare o eseguire l'azione esclusivamente se dispone di informazioni personalizzate, non generiche, sull'azione specifica. Le azioni proprietarie non vengono restituite all'applicazione client, a meno che l'applicazione client richiede in modo esplicito, impostando la restrizione appropriata sul **APPLICATION_NAME**.|  
  
## <a name="invocation-types"></a>Tipi di chiamate  
 Nella tabella seguente vengono descritti i diversi tipi di chiamate disponibili in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Il tipo di chiamata viene utilizzato dall'applicazione client solo per determinare quando richiamare l'azione, ma non determina effettivamente il comportamento di chiamata dell'azione.  
  
|Tipo di chiamata|Descrizione|  
|---------------------|-----------------|  
|**INTERATTIVO**|L'azione deve essere richiamata dall'applicazione client tramite l'interazione dell'utente.|  
|**ON_OPEN**|L'azione deve essere richiamata dall'applicazione client quando viene aperto l'oggetto di destinazione. Questo tipo di chiamata non è attualmente implementato.|  
|**BATCH**|L'azione deve essere richiamata dall'applicazione client quando l'oggetto di destinazione è coinvolto in un'operazione batch, secondo quanto determinato dall'applicazione client. Questo tipo di chiamata non è attualmente implementato.|  
  
### <a name="scope"></a>`Scope`  
 Ogni azione è definita per un cubo specifico e ha un nome univoco in tale cubo. Un'azione può avere uno degli ambiti elencati nella tabella seguente.  
  
 Ambito cubo  
 Per azioni indipendenti da dimensioni specifiche, i membri o le celle; Per esempio: "Emulazione di terminale per avviare AS/400 sistema di produzione".  
  
 Ambito dimensione  
 L'azione viene applicata a una dimensione specifica. Le azioni di questo tipo non dipendono dagli specifici livelli o membri selezionati.  
  
 Ambito livello  
 L'azione viene applicata a un livello di dimensione specifico. Le azioni di questo tipo non dipendono dallo specifico membro selezionato nella dimensione.  
  
 Ambito membro  
 L'azione viene applicata a membri specifici di un livello.  
  
 Ambito cella  
 L'azione viene applicata solo a celle specifiche.  
  
 Ambito set  
 L'azione viene applicata solo a un set. Il nome **ActionParameterSet**, è riservato per usi dall'applicazione all'interno dell'espressione dell'azione.  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzioni di definizione dei dati MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
