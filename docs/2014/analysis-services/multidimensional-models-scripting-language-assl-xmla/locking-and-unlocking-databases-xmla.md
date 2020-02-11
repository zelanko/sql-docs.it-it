---
title: Blocco e sblocco di database (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- locking [XML for Analysis]
- XML for Analysis, locking
- XMLA, locking
- unlocking objects
ms.assetid: 451afa58-ce03-4ecc-8dd3-9e7e8559b5f1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 290f1e5fe7efb876ab6c24004c7465cf109de0d0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62702225"
---
# <a name="locking-and-unlocking-databases-xmla"></a>Blocco e sblocco di database (XMLA)
  È possibile bloccare e sbloccare i database utilizzando, rispettivamente, i comandi [Lock](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) e [Unlock](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) in XML for Analysis (XMLA). In genere, gli altri comandi XMLA bloccano e sbloccano automaticamente gli oggetti in base alle esigenze per completare il comando durante l'esecuzione. È possibile bloccare o sbloccare in modo esplicito un database per eseguire più comandi all'interno di una singola transazione, ad esempio un comando [batch](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla) , impedendo ad altre applicazioni di eseguire il commit di una transazione di scrittura nel database.  
  
## <a name="locking-databases"></a>Blocco di database  
 Il comando `Lock` blocca un oggetto, per utilizzo condiviso o esclusivo, all'interno del contesto della transazione attualmente attiva. Un blocco su un oggetto impedisce alle transazioni di eseguire il commit finché non viene rimosso. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta due tipi di blocchi, blocchi condivisi e blocchi esclusivi. Per ulteriori informazioni sui tipi di blocco supportati da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vedere [elemento Mode &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/mode-element-xmla).  
  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] consente solo che i database vengano bloccati. L'elemento [oggetto](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) deve contenere un riferimento a un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oggetto database. Se l'elemento `Object` non viene specificato oppure fa riferimento a un oggetto diverso da un database `Object`, si verifica un errore.  
  
> [!IMPORTANT]  
>  Solo amministratori del database o amministratori del server possono eseguire in modo esplicito un comando `Lock`.  
  
 Gli altri comandi eseguono implicitamente un comando `Lock` su un database [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Qualsiasi operazione che legge dati o metadati da un database, ad esempio qualsiasi metodo [Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) o un metodo [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) che esegue un comando [Statement](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) , emette implicitamente un blocco condiviso sul database. Qualsiasi transazione che esegue il commit delle modifiche nei dati o nei metadati in un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oggetto di un database, `Execute` ad esempio un metodo che esegue un comando [ALTER](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla) , emette in modo implicito un blocco esclusivo sul database.  
  
## <a name="unlocking-objects"></a>Sblocco di oggetti  
 Il comando `Unlock` rimuove un blocco applicato all'interno del contesto della transazione attualmente attiva.  
  
> [!IMPORTANT]  
>  Solo gli amministratori del database o gli amministratori del server possono eseguire in modo esplicito un comando `Unlock`.  
  
 Tutti i blocchi sono contenuti nel contesto della transazione corrente. Quando viene eseguito il commit oppure il rollback della transazione corrente, tutti i blocchi definiti all'interno della transazione vengono rilasciati automaticamente.  
  
## <a name="see-also"></a>Vedere anche  
 [Elemento Lock &#40;&#41;XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)   
 [Elemento Unlock &#40;&#41;XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)   
 [Sviluppo con XMLA in Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
