---
title: Uso di variabili nel componente script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], using variables
ms.assetid: 92d1881a-1ef1-43ae-b1ca-48d0536bdbc2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: bb913313c77ca98cb3155afa73aab533918fd3de
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85426058"
---
# <a name="using-variables-in-the-script-component"></a>Utilizzo di variabili nel componente script
  Nelle variabili vengono archiviati valori che possono essere utilizzati in fase di esecuzione da un pacchetto e dai relativi contenitori, attività e gestori eventi. Per altre informazioni, vedere [Variabili di Integration Services &#40;SSIS&#41;](../../integration-services-ssis-variables.md).  
  
 È possibile rendere disponibili le variabili esistenti per l'accesso in sola lettura o in lettura/scrittura da parte dello script personalizzato immettendo elenchi di variabili delimitate da virgole nei `ReadOnlyVariables` `ReadWriteVariables` campi e della pagina **script** di **Editor trasformazione script**. Tenere presente che per i nomi delle variabili viene applicata la distinzione tra maiuscole e minuscole. Utilizzare la proprietà `Value` per leggere e scrivere in singole variabili. Il componente script gestisce automaticamente l'eventuale blocco richiesto mentre lo script modifica le variabili in fase di esecuzione.  
  
> [!IMPORTANT]  
>  La raccolta di `ReadWriteVariables` è disponibile solo nel metodo `PostExecute` per aumentare le prestazioni e ridurre il rischio di conflitti di blocco. Pertanto, non è possibile incrementare direttamente il valore di una variabile del pacchetto durante l'elaborazione di ogni riga di dati. Al contrario, incrementare il valore di una variabile locale e impostare il valore della variabile del pacchetto sul valore della variabile locale nel metodo `PostExecute` dopo l'elaborazione di tutti i dati. È anche possibile utilizzare la proprietà <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> per ovviare a questa limitazione, come descritto più avanti in questo argomento. Tuttavia, se si scrive direttamente in una variabile del pacchetto durante l'elaborazione di ogni riga, si verificano effetti negativi sulle prestazioni e aumenta il rischio di conflitti di blocco.  
  
 Per altre informazioni sulla pagina **Script** dell'**Editor trasformazione Script**, vedere [Configurazione del componente script nell'editor corrispondente](configuring-the-script-component-in-the-script-component-editor.md) ed [Editor trasformazione Script &#40;pagina Script&#41;](../../script-transformation-editor-script-page.md).  
  
 Il componente script crea una classe di raccolta `Variables` nell'elemento di progetto `ComponentWrapper` con una proprietà di funzione di accesso fortemente tipizzata per il valore di ogni variabile preconfigurata, in cui la proprietà ha lo stesso nome della variabile stessa. Questa raccolta viene esposta tramite la proprietà `Variables` della classe `ScriptMain`. La proprietà della funzione di accesso fornisce autorizzazioni di sola lettura o di lettura/scrittura al valore della variabile, a seconda dei casi. Se ad esempio è stata aggiunta una variabile integer denominata `MyIntegerVariable` all'elenco `ReadOnlyVariables`, è possibile recuperarne il valore nello script tramite il codice seguente:  
  
 `Dim myIntegerVariableValue As Integer = Me.Variables.MyIntegerVariable`  
  
 È anche possibile utilizzare la proprietà <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A>, accessibile tramite una chiamata a `Me.VariableDispenser`, per utilizzare le variabili nel componente script. In questo caso, non si utilizzano le proprietà delle funzioni di accesso tipizzate e denominate per le variabili, ma si accede alle variabili direttamente. Quando si utilizza <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A>, è necessario gestire sia la semantica di blocco che il cast dei tipi di dati per i valori delle variabili nel codice personalizzato. È necessario utilizzare la proprietà <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> anziché le proprietà delle funzioni di accesso denominate e tipizzate se si desidera utilizzare una variabile non disponibile in fase di progettazione ma che viene creata a livello di codice in fase di esecuzione.  
  
![Integration Services icona (piccola)](../../media/dts-16.gif "Icona di Integration Services (piccola)")  **rimane aggiornata con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visitare la pagina relativa a Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services &#40;variabili&#41; SSIS](../../integration-services-ssis-variables.md)   
 [Utilizzo di variabili nei pacchetti](../../use-variables-in-packages.md)  
  
  
