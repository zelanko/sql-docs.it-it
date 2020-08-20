---
description: MSSQLSERVER_511
title: MSSQLSERVER_511 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 511 (Database Engine error)
ms.assetid: 0c85686a-53c1-4180-ba8c-2000e68a0d63
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: beb8f25c2251904f84f358012a5e1ad26450abfd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471058"
---
# <a name="mssqlserver_511"></a>MSSQLSERVER_511
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
|Nome prodotto|SQL Server|  
|ID evento|511|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|ROW_TOOBIG|  
|Testo del messaggio|Impossibile creare una riga con dimensioni %d, perché tale valore è maggiore delle dimensioni massime consentite %d.|  
  
## <a name="explanation"></a>Spiegazione  
L'operazione tentata ha provocato il superamento delle dimensioni massime di una riga. rappresentate in genere dal valore 8.060 byte. Alcuni formati di archiviazione contengono overhead che può ridurre le dimensioni della riga disponibili per i dati. Se si utilizzano colonne di tipo sparse, ad esempio, il valore delle dimensioni massime di una riga è di 8.018 byte. Per alcune operazioni che aggiungono o rimuovono righe e per altre che modificano il tipo di dati di una colonna è necessario riscrivere la riga nella pagina di dati, quindi rimuovere riga originale. Per queste operazioni, il limite effettivo alla dimensioni della riga è la metà di quello massimo consentito, poiché la riga originale e quella modificata devono essere contenute entrambe nella pagina di dati per un breve periodo di tempo.  
  
## <a name="user-action"></a>Azione dell'utente  
Se possibile, ridurre le dimensioni della riga.  
  
Se si ritiene che il problema sia causato da un aggiornamento sul posto della riga, è necessario modificare la tabella in più passaggi. Creare una nuova tabella e trasferirvi i dati. Successivamente eliminare la tabella originale e rinominare la nuova tabella oppure troncare la tabella originale, modificarne le righe, quindi spostarvi nuovamente i dati.  
  
