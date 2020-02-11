---
title: Gestione delle transazioni (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- XML for Analysis, transactions
- XMLA, transactions
- explicit transactions [XMLA]
- implicit transactions
- transactions [XML for Analysis]
- rolling back transactions, XMLA
- reference counts [XML for Analysis]
- committing transactions
- starting transactions
ms.assetid: f5112e01-82f8-4870-bfb7-caa00182c999
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ad8a77d1d8552dc811c1232afb53c142452658db
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62727218"
---
# <a name="managing-transactions-xmla"></a>Gestione di transazioni (XMLA)
  Ogni comando XML for Analysis (XMLA) inviato a un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene eseguito nel contesto di una transazione nella sessione implicita o esplicita corrente. Per gestire ognuna di queste transazioni, usare i comandi [BeginTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/begintransaction-element-xmla), [CommitTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/committransaction-element-xmla)e [RollbackTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/rollbacktransaction-element-xmla) . che consentono di creare transazioni implicite o esplicite, modificare il conteggio dei riferimenti alla transazione nonché di avviare le transazioni ed eseguirne il commit e il rollback.  
  
## <a name="implicit-and-explicit-transactions"></a>Transazioni implicite ed esplicite  
 Una transazione può essere implicita o esplicita, come descritto di seguito.  
  
 **Transazione implicita**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]Crea una transazione *implicita* per un comando XMLA se `BeginTransaction` il comando non specifica l'inizio di una transazione. 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esegue sempre il commit di una transazione implicita se il comando riesce e ne esegue il rollback se il comando non riesce.  
  
 **Transazione esplicita**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]Crea una transazione *esplicita* se `BeginTransaction` il comando avvia una transazione. 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tuttavia esegue il commit di una transazione esplicita solo se viene inviato un comando `CommitTransaction` e ne esegue il rollback se viene inviato un comando `RollbackTransaction`.  
  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] inoltre esegue il rollback sia di transazioni implicite che di transazioni esplicite se la sessione corrente termina prima del completamento della transazione attiva.  
  
## <a name="transactions-and-reference-counts"></a>Transazioni e conteggi dei riferimenti  
 In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene gestito un conteggio dei riferimenti alla transazione per ogni sessione. 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] non supporta tuttavia transazioni nidificate poiché per ogni sessione viene gestita una sola transazione attiva. Se nella sessione corrente non è presente una transazione attiva, il conteggio dei riferimenti alla transazione è impostato su zero.  
  
 In altri termini, ogni comando `BeginTransaction` incrementa il conteggio dei riferimenti di uno, mentre ogni comando `CommitTransaction` decrementa il conteggio dei riferimenti sempre di uno. Se un comando `CommitTransaction` imposta il conteggio relativo alla transazione su zero, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esegue il commit della transazione.  
  
 Il comando `RollbackTransaction` esegue tuttavia il rollback della transazione attiva indipendentemente dal valore corrente del conteggio dei riferimenti alla transazione. In altri termini, un unico comando `RollbackTransaction` esegue il rollback della transazione attiva, indipendentemente dal numero di comandi `BeginTransaction` o `CommitTransaction` inviati e imposta il conteggio dei riferimenti alla transazione su zero.  
  
## <a name="beginning-a-transaction"></a>Avvio di una transazione.  
 Il comando `BeginTransaction` avvia una transazione esplicita nella sessione corrente e incrementa di uno il conteggio dei riferimenti alla transazione per la sessione corrente. Tutti i comandi successivi vengono considerati all'interno della transazione attiva, fino a quando non viene inviato un numero sufficiente di comandi `CommitTransaction` per eseguire il commit della transazione attiva o non viene inviato un unico comando `RollbackTransaction` per eseguirne il rollback.  
  
## <a name="committing-a-transaction"></a>Esecuzione del commit di una transazione  
 Il comando `CommitTransaction` esegue il commit dei risultati di comandi eseguiti dopo che il comando `BeginTransaction` è stato eseguito nella sessione corrente. Ogni comando `CommitTransaction` decrementa il conteggio dei riferimenti per le transazioni attive in una sessione. Se un comando `CommitTransaction` imposta il conteggio dei riferimenti su zero, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esegue il commit della transazione attiva. Se non è presente alcuna transazione attiva, ovvero se il conteggio dei riferimenti alla transazione per la sessione corrente è già impostato su zero, un comando `CommitTransaction` restituisce un errore.  
  
## <a name="rolling-back-a-transaction"></a>Esecuzione del rollback di una transazione  
 Il comando `RollbackTransaction` esegue il rollback dei risultati di comandi eseguiti dopo che il comando `BeginTransaction` è stato eseguito nella sessione corrente. Il comando `RollbackTransaction` esegue il rollback della transazione attiva indipendentemente dal valore corrente del conteggio dei riferimenti alla transazione e imposta tale conteggio su zero. Se non è presente alcuna transazione attiva, ovvero se il conteggio dei riferimenti alla transazione per la sessione corrente è già impostato su zero, un comando `RollbackTransaction` restituisce un errore.  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo con XMLA in Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
