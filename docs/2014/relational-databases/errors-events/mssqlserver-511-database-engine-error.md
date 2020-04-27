---
title: MSSQLSERVER_511 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 511 (Database Engine error)
ms.assetid: 0c85686a-53c1-4180-ba8c-2000e68a0d63
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ee53135fb492185d91287f553b7b1f0ddf3cc8ba
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62867796"
---
# <a name="mssqlserver_511"></a>MSSQLSERVER_511
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|511|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|ROW_TOOBIG|  
|Testo del messaggio|Impossibile creare una riga con dimensioni %d, perché tale valore è maggiore delle dimensioni massime consentite %d.|  
  
## <a name="explanation"></a>Spiegazione  
 L'operazione tentata ha provocato il superamento delle dimensioni massime di una riga. rappresentate in genere dal valore 8.060 byte. Alcuni formati di archiviazione contengono overhead che può ridurre le dimensioni della riga disponibili per i dati. Se si utilizzano colonne di tipo sparse, ad esempio, il valore delle dimensioni massime di una riga è di 8.018 byte. Per alcune operazioni che aggiungono o rimuovono righe e per altre che modificano il tipo di dati di una colonna è necessario riscrivere la riga nella pagina di dati, quindi rimuovere riga originale. Per queste operazioni, il limite effettivo alla dimensioni della riga è la metà di quello massimo consentito, poiché la riga originale e quella modificata devono essere contenute entrambe nella pagina di dati per un breve periodo di tempo.  
  
> [!WARNING]  
>  Ogni colonna non Null **varchar(max)** o **nvarchar(max)** richiede 24 byte di allocazione fissa aggiuntiva che concorre al raggiungimento del limite delle righe di 8.060 byte durante un'operazione di ordinamento. Ciò può creare un limite implicito al numero di colonne non Null **varchar(max)** o **nvarchar(max)** che è possibile creare in una tabella. Non vengono segnalati errori particolari (oltre il normale avviso che indica che le dimensioni massime per le righe superano il valore massimo consentito di 8060 byte) durante la creazione della tabella o l'inserimento dei dati. Queste dimensioni delle righe eccessive possono causare errori (ad esempio, l'errore 512) durante le normali operazioni, ad esempio un aggiornamento della chiave dell'indice cluster o l'ordinamento del set di colonne completo, che gli utenti non possono prevedere finché non eseguono un'operazione.  
  
## <a name="user-action"></a>Azione dell'utente  
 Se possibile, ridurre le dimensioni della riga.  
  
 Se si ritiene che il problema sia causato da un aggiornamento sul posto della riga, è necessario modificare la tabella in più passaggi. Creare una nuova tabella e trasferirvi i dati. Successivamente eliminare la tabella originale e rinominare la nuova tabella oppure troncare la tabella originale, modificarne le righe, quindi spostarvi nuovamente i dati.  
  
  
