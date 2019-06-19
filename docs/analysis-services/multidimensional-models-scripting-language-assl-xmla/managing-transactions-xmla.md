---
title: La gestione delle transazioni (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6c85b1f9db4667c64bed7cf87189e48b507e5f75
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63055076"
---
# <a name="managing-transactions-xmla"></a>Gestione di transazioni (XMLA)
  Ogni comando XML for Analysis (XMLA) inviato a un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene eseguito all'interno del contesto di una transazione nella sessione implicita o esplicita corrente. Per gestire ognuna di queste transazioni, si utilizza il [BeginTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/begintransaction-element-xmla), [CommitTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/committransaction-element-xmla), e [RollbackTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/rollbacktransaction-element-xmla) comandi. che consentono di creare transazioni implicite o esplicite, modificare il conteggio dei riferimenti alla transazione nonché di avviare le transazioni ed eseguirne il commit e il rollback.  
  
## <a name="implicit-and-explicit-transactions"></a>Transazioni implicite ed esplicite  
 Una transazione può essere implicita o esplicita, come descritto di seguito.  
  
 **transazione implicita**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Crea un' *implicita* transazione per un XMLA comando se il **BeginTransaction** comando non specifica l'inizio di una transazione. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esegue sempre il commit di una transazione implicita se il comando riesce e ne esegue il rollback se il comando non riesce.  
  
 **transazione esplicita**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Crea un' *esplicite* transazione se il **BeginTransaction** comando avvia una transazione. Tuttavia [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esegue il commit solo una transazione esplicita se un **CommitTransaction** comando viene inviato e rollback di una transazione esplicita se una **RollbackTransaction** comando viene inviato.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] inoltre esegue il rollback sia di transazioni implicite che di transazioni esplicite se la sessione corrente termina prima del completamento della transazione attiva.  
  
## <a name="transactions-and-reference-counts"></a>Transazioni e conteggi dei riferimenti  
 In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene gestito un conteggio dei riferimenti alla transazione per ogni sessione. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] non supporta tuttavia transazioni nidificate poiché per ogni sessione viene gestita una sola transazione attiva. Se nella sessione corrente non è presente una transazione attiva, il conteggio dei riferimenti alla transazione è impostato su zero.  
  
 In altre parole, ognuna **BeginTransaction** comando incrementa il conteggio dei riferimenti di uno, mentre ogni **CommitTransaction** comando decrementa il conteggio riferimenti da uno. Se un **CommitTransaction** comando imposta il numero di transazioni a zero, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] il commit della transazione.  
  
 Tuttavia, il **RollbackTransaction** comando esegue il rollback della transazione attiva indipendentemente dal valore corrente del conteggio dei riferimenti delle transazioni. In altre parole, un singolo **RollbackTransaction** comando esegue il rollback della transazione attiva, indipendentemente da quante **BeginTransaction** comandi oppure **CommitTransaction** i comandi sono stati inviati e imposta tale conteggio su zero.  
  
## <a name="beginning-a-transaction"></a>Avvio di una transazione.  
 Il **BeginTransaction** comando avvia una transazione esplicita nella sessione corrente e incrementa il conteggio dei riferimenti delle transazioni per la sessione corrente di uno. Tutti i comandi successivi vengono considerati all'interno della transazione attiva, fino a quando non sufficiente **CommitTransaction** vengono inviati i comandi per eseguire il commit della transazione attiva o una singola **RollbackTransaction**Invia comando per eseguire il rollback della transazione attiva.  
  
## <a name="committing-a-transaction"></a>Esecuzione del commit di una transazione  
 Il **CommitTransaction** comando esegue il commit dei risultati di comandi che vengono eseguiti dopo le **BeginTransaction** comando è stato eseguito nella sessione corrente. Ciascuna **CommitTransaction** comando decrementa il conteggio dei riferimenti per le transazioni attive su una sessione. Se un **CommitTransaction** comando imposta il conteggio dei riferimenti su zero, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esegue il commit della transazione attiva. Se non sono presenti transazioni attive (in altre parole, il conteggio dei riferimenti delle transazioni per la sessione corrente è già impostato su zero), un **CommitTransaction** comando genera un errore.  
  
## <a name="rolling-back-a-transaction"></a>Esecuzione del rollback di una transazione  
 Il **RollbackTransaction** comando esegue il rollback dei risultati di comandi che vengono eseguiti dopo le **BeginTransaction** comando è stato eseguito nella sessione corrente. Il **RollbackTransaction** comando esegue il rollback della transazione attiva, indipendentemente dal fatto il conteggio dei riferimenti alla transazione corrente e imposta il conteggio dei riferimenti delle transazioni su zero. Se non sono presenti transazioni attive (in altre parole, il conteggio dei riferimenti delle transazioni per la sessione corrente è già impostato su zero), un **RollbackTransaction** comando genera un errore.  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo con XMLA in Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
