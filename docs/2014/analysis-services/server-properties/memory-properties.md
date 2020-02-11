---
title: Proprietà memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- LowMemoryLimit property
- MinimumAllocatedMemory property
- MidMemoryPrice property
- MemoryHeapType property
- memory [Analysis Services]
- DefaultPagesCountToReuse property
- TotalMemoryLimit property
- SessionMemoryLimit property
- VirtualMemoryLimit property
- WaitCountIfHighMemory property
- HighMemoryPrice property
- HeapTypeForObjects property
ms.assetid: 085f5195-7b2c-411a-9813-0ff5c6066d13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a88e2c1508ec849437d90b3de7c66705299dafc1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66068886"
---
# <a name="memory-properties"></a>Proprietà della memoria
  
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta le proprietà della memoria del server elencate nella tabella seguente. Per le linee guida di impostazione di queste proprietà, vedere la [Guida operativa di SQL Server 2008 R2 Analysis Services](https://go.microsoft.com/fwlink/?LinkID=225539).  
  
 I valori compresi tra 1 e 100 rappresentano le percentuali di **memoria fisica totale** o **spazio degli indirizzi virtuali**, a seconda di quale dei due elementi sia inferiore. I valori maggiori di 100 rappresentano limiti di memoria in byte.  
  
 **Si applica a:** Modalità server multidimensionale e tabulare, se non specificato diversamente.  
  
## <a name="properties"></a>Proprietà  
 `LowMemoryLimit`  
 Proprietà con numero a virgola mobile e precisione doppia a 64 bit con segno che definisce il punto in cui il server sta esaurendo la memoria, espresso come percentuale della memoria fisica totale. Quando viene raggiunto questo limite, verrà avviata la cancellazione della memoria delle cache da parte dell'istanza, chiudendo le sessioni scadute e scaricando i calcoli inusati. Il server non rilascerà memoria al di sotto di questo limite. Il valore predefinito è 65 e indica che il limite inferiore della memoria è il 65% della memoria fisica o dello spazio di indirizzo virtuale, a seconda di quale dei due elementi sia inferiore.  
  
 `TotalMemoryLimit`  
 Definisce una soglia che, una volta raggiunta, induce il server a deallocare la memoria in maniera più drastica. Il valore predefinito è 80% della memoria fisica o dello spazio di indirizzo virtuale, a seconda di quale dei due elementi sia inferiore.  
  
 Si noti che `TotalMemoryLimit` deve essere sempre minore di `HardMemoryLimit`  
  
 `HardMemoryLimit`  
 Specifica una soglia di memoria superata la quale le sessioni utente attive verranno immediatamente terminate dall'istanza per ridurre l'utilizzo della memoria. Per tutte le sessioni terminate verrà visualizzato un errore che indica l'annullamento a causa di un numero eccessivo di richieste di memoria. Con il valore predefinito, ovvero zero (0), il limite `HardMemoryLimit` sarà impostato su un valore mediano tra `TotalMemoryLimit` e la memoria fisica totale del sistema; se quest'ultima è maggiore dello spazio di indirizzo virtuale del processo, per calcolare il limite `HardMemoryLimit` sarà invece usato lo spazio di indirizzo virtuale.  
  
 `VirtualMemoryLimit`  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `VertiPaqPagingPolicy`  
 Specifica il comportamento di paging nel caso in cui la memoria del server sia insufficiente. I valori validi sono i seguenti:  
  
 Zero (**0**) Disabilita il paging. Se la memoria è insufficiente, l'elaborazione ha esito negativo e provoca un errore memoria insufficiente. Se si disabilita il paging, è necessario concedere i privilegi di Windows all'account del servizio. Per istruzioni, vedere [Configurare gli account del servizio &#40;Analysis Services&#41;](../instances/configure-service-accounts-analysis-services.md).  
  
 **1** è il valore predefinito. Questa proprietà abilita il paging su disco utilizzando il file di paging del sistema operativo (pagefile.sys).  
  
 Quando `VertiPaqPagingPolicy` è impostato su 1, è meno probabile che l'elaborazione non venga completata a causa di limitazioni di memoria perché il server tenterà di eseguire il paging su disco utilizzando il metodo specificato. L'impostazione della proprietà `VertiPaqPagingPolicy` non garantisce che non si verificheranno mai gli errori della memoria. Gli errori di memoria insufficiente si possono comunque verificare nelle condizioni seguenti:  
  
-   Non c'è abbastanza memoria per tutti i dizionari. Durante l'elaborazione, Analysis Services blocca i dizionari per ogni colonna in memoria e tutti i dizionari insieme non possono essere maggiori del valore specificato per `VertiPaqMemoryLimit`.  
  
-   Lo spazio dell'indirizzo virtuale è insufficiente per il processo.  
  
 Per risolvere gli errori di memoria insufficiente persistenti è possibile riprogettare il modello per ridurre la quantità di dati che devono essere elaborati oppure è possibile aggiungere più memoria fisica al computer.  
  
 Questo metodo si applica solo in modalità server tabulare.  
  
 `VertiPaqMemoryLimit`  
 Se il paging su disco è consentito, questa proprietà consente di specificare il livello di consumo di memoria (come percentuale della memoria totale) da cui avrà inizio il paging. Il valore predefinito è 60. Se il consumo di memoria è inferiore al 60%, il server non eseguirà il paging su disco.  
  
 Questa proprietà dipende da `VertiPaqPagingPolicyProperty`che deve essere impostata su 1 affinché si verifichi il paging.  
  
 Questo metodo si applica solo in modalità server tabulare.  
  
 `HighMemoryPrice`  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `MemoryHeapType`  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 Questo metodo si applica solo in modalità server multidimensionale.  
  
 `HeapTypeForObjects`  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 Questo metodo si applica solo in modalità server multidimensionale.  
  
 `DefaultPagesCountToReuse`  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `HandleIA64AlignmentFaults`  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `MidMemoryPrice`  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `MinimumAllocatedMemory`  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `PreAllocate`  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `SessionMemoryLimit`  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `WaitCountIfHighMemory`  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare le proprietà del server in Analysis Services](server-properties-in-analysis-services.md)   
 [Determinare la modalità server di un'istanza di Analysis Services](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
