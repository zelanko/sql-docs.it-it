---
description: Utilizzo di variabili nel componente script
title: Uso di variabili nel componente script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], using variables
ms.assetid: 92d1881a-1ef1-43ae-b1ca-48d0536bdbc2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d27181eac591f6c66166810e9662c04b6b97fc40
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/26/2020
ms.locfileid: "92196420"
---
# <a name="using-variables-in-the-script-component"></a>Utilizzo di variabili nel componente script

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  Nelle variabili vengono archiviati valori che possono essere utilizzati in fase di esecuzione da un pacchetto e dai relativi contenitori, attività e gestori eventi. Per altre informazioni, vedere [Variabili di Integration Services &#40;SSIS&#41;](../../../integration-services/integration-services-ssis-variables.md).  
  
 È possibile rendere disponibili le variabili esistenti per l'accesso di sola lettura o di lettura/scrittura da parte dello script personalizzato immettendo elenchi di variabili delimitate da virgole nei campi **ReadOnlyVariables** e **ReadWriteVariables** della pagina **Script** dell'**Editor trasformazione Script**. Tenere presente che per i nomi delle variabili viene applicata la distinzione tra maiuscole e minuscole. Usare la proprietà **Value** per leggere e scrivere in singole variabili. Il componente script gestisce automaticamente l'eventuale blocco richiesto mentre lo script modifica le variabili in fase di esecuzione.  
  
> [!IMPORTANT]  
>  La raccolta di **ReadWriteVariables** è disponibile solo nel metodo **PostExecute** per ottimizzare le prestazioni e ridurre il rischio di conflitti di blocco. Pertanto, non è possibile incrementare direttamente il valore di una variabile del pacchetto durante l'elaborazione di ogni riga di dati. Incrementare invece il valore di una variabile locale e impostare il valore della variabile del pacchetto sul valore della variabile locale nel metodo **PostExecute** dopo che tutti i dati sono stati elaborati. È anche possibile utilizzare la proprietà <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> per ovviare a questa limitazione, come descritto più avanti in questo argomento. Tuttavia, se si scrive direttamente in una variabile del pacchetto durante l'elaborazione di ogni riga, si verificano effetti negativi sulle prestazioni e aumenta il rischio di conflitti di blocco.  
  
 Per altre informazioni sulla pagina **Script** dell'**Editor trasformazione Script**, vedere [Configurazione del componente script nell'editor corrispondente](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md) ed [Editor trasformazione Script &#40;pagina Script&#41;](../../data-flow/transformations/script-component.md).  
  
 Il componente script crea una classe di raccolta **Variables** nell'elemento di progetto **ComponentWrapper** con una proprietà di funzione di accesso fortemente tipizzata per il valore di ogni variabile preconfigurata, in cui la proprietà ha lo stesso nome della variabile stessa. La raccolta viene esposta tramite la proprietà **Variables** della classe **ScriptMain**. La proprietà della funzione di accesso fornisce autorizzazioni di sola lettura o di lettura/scrittura al valore della variabile, a seconda dei casi. Se ad esempio è stata aggiunta una variabile di tipo integer denominata `MyIntegerVariable` all'elenco **ReadOnlyVariables**, è possibile recuperarne il valore nello script tramite il codice seguente:  
  
 `Dim myIntegerVariableValue As Integer = Me.Variables.MyIntegerVariable`  
  
 È anche possibile utilizzare la proprietà <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A>, accessibile tramite una chiamata a `Me.VariableDispenser`, per utilizzare le variabili nel componente script. In questo caso, non si utilizzano le proprietà delle funzioni di accesso tipizzate e denominate per le variabili, ma si accede alle variabili direttamente. Quando si utilizza <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A>, è necessario gestire sia la semantica di blocco che il cast dei tipi di dati per i valori delle variabili nel codice personalizzato. È necessario utilizzare la proprietà <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> anziché le proprietà delle funzioni di accesso denominate e tipizzate se si desidera utilizzare una variabile non disponibile in fase di progettazione ma che viene creata a livello di codice in fase di esecuzione.  
  
## <a name="see-also"></a>Vedere anche  
 [Variabili di Integration Services &#40;SSIS&#41;](../../../integration-services/integration-services-ssis-variables.md)   
 [Uso di variabili nei pacchetti](../../integration-services-ssis-variables.md)  
  
