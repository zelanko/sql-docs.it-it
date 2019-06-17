---
title: L'elaborazione delle transazioni | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- transactions [ADO]
- data updates [ADO], transaction processing
- updating data [ADO], transaction processing
- nested transactions [ADO]
ms.assetid: 74ab6706-e2dc-42cb-af77-dbc58a9cf4ce
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 032677452fa80502d37383af8172ff9475dea363
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704817"
---
# <a name="transaction-processing"></a>Elaborazione di transazioni
Oggetto *transazione* delimita l'inizio e alla fine di una serie di operazioni di accesso ai dati eseguite attraverso una connessione. Soggetti alle funzionalità transazionali di origine dati, il **connessione** oggetto consente inoltre di creare e gestire le transazioni. Ad esempio, Usa il Provider Microsoft OLE DB per SQL Server per accedere a un database in Microsoft SQL Server, è possibile creare più transazioni nidificate per i comandi da eseguire.  
  
 ADO assicura che si verificano modifiche a un'origine dei dati risultanti dalle operazioni in una transazione correttamente tra loro o non ereditarli affatto.  
  
 Se si annulla la transazione o una delle relative operazioni non riesce, il risultato è come se nessuna delle operazioni nella transazione si è verificato. L'origine dati rimarranno com'era prima dell'inizio della transazione.  
  
 ADO fornisce i metodi seguenti per la gestione delle transazioni: **BeginTrans**, **CommitTrans**, e **RollbackTrans**. Usare questi metodi con un **connessione** dell'oggetto quando si desidera salvare o annullare una serie di modifiche apportate ai dati di origine come singola unità. Ad esempio, per il trasferimento di denaro tra conti, si sottrae un importo da uno e si aggiunge la stessa quantità a altro. Se l'aggiornamento ha esito negativo, l'account non è più bilanciare. Queste modifiche all'interno di una transazione aperta assicura che passano attraverso tutte o nessuna delle modifiche.  
  
> [!NOTE]
>  Non tutti i provider supportano le transazioni. Verificare che la proprietà definito dal provider "**transazione DDL**" viene visualizzato nei **connessione** dell'oggetto [proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) raccolta, che indica che il provider supporta transazioni. Se il provider non supporta le transazioni, una chiamata a uno di questi metodi restituirà un errore.  
  
 Dopo aver chiamato il **BeginTrans** metodo, il provider non è più istantaneamente verrà commit le modifiche apportate fino a quando non si chiama **CommitTrans** oppure **RollbackTrans** per terminare il transazione.  
  
 Chiama il **CommitTrans** metodo salva le modifiche apportate all'interno di una transazione aperta per la connessione e termina la transazione. Chiama il **RollbackTrans** metodo inverte le modifiche apportate all'interno di una transazione aperta e termina la transazione. La chiamata a dei metodi quando non sono presenti transazioni aperte genera un errore.  
  
 In base il **connessione** dell'oggetto [attributi](../../../ado/reference/ado-api/attributes-property-ado.md) proprietà, la chiamata al **CommitTrans** o **RollbackTrans** potrebbe (metodo) avviare automaticamente una nuova transazione. Se il **attributi** è impostata su **adXactCommitRetaining**, il provider avvia automaticamente una nuova transazione dopo un **CommitTrans** chiamare. Se il **attributi** è impostata su **adXactAbortRetaining**, il provider avvia automaticamente una nuova transazione dopo un **RollbackTrans** chiamare.  
  
## <a name="transaction-isolation-level"></a>Livello di isolamento della transazione  
 Usare la **IsolationLevel** per impostare il livello di isolamento di una transazione in un **connessione** oggetto. L'impostazione ha effetto fino al successivo si chiama il [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) (metodo). Se il livello di isolamento che richiesto non è disponibile, il provider può restituire il successivo livello più alto di isolamento. Vedere le **IsolationLevel** proprietà nel riferimento del programmatore di ADO per ulteriori informazioni sui valori validi.  
  
## <a name="nested-transactions"></a>Transazioni nidificate  
 Per i provider che supportano le transazioni nidificate, chiama il **BeginTrans** metodo all'interno di una transazione aperta inizia una nuova transazione nidificata. Il valore restituito indica il livello di annidamento: indica un valore restituito pari a "1" è stata aperta una transazione di primo livello (vale a dire, la transazione non è annidata all'interno di un'altra transazione), "2" indica che è stato aperto una transazione di secondo livello (una transazione annidata all'interno di una transazione di primo livello), e così via. La chiamata **CommitTrans** oppure **RollbackTrans** interessa solo la maggior parte delle transazioni aperti di recente; è necessario chiudere o il rollback della transazione corrente prima che è possibile risolvere alcuna transazione di livello superiore.
