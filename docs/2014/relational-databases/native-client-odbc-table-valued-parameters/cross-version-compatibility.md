---
title: Compatibilità tra versioni | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), cross-version compatibility
ms.assetid: 5f14850b-b85c-41e2-8116-6f5b3f5e0856
author: rothja
ms.author: jroth
ms.openlocfilehash: af434713946f5c568ee71644a7403f9496a8c16f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049707"
---
# <a name="cross-version-compatibility"></a>Compatibilità tra versioni
  Possono verificarsi conflitti tra versioni quando è previsto che istanze client o server di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] elaborino parametri con valori di tabella.  
  
 In generale, la funzionalità dei parametri con valori di tabella è disponibile solo per i client [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] che utilizzano SQL Server Native Client 10.0 o versione successiva e che sono connessi a server [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o versione successiva. Le nuove colonne nei set di risultati della funzione Catalog saranno presenti solo quando si è connessi a un [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Server (o versioni successive).  
  
 Se un'applicazione client compilata con una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client esegue istruzioni per le quali sono previsti parametri con valori di tabella, il server rileva questa condizione mediante un errore di conversione dei dati e ODBC restituisce l'errore SQLSTATE 07006 e il messaggio "Violazione dell'attributo del tipo di dati".  
  
 Se un'applicazione client compilata con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client 10,0 o versioni successive tenta di utilizzare parametri con valori di tabella quando si è connessi a un'istanza del server precedente a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] , [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client rileverà il problema e le chiamate a SQLBindCol, SQLBindParameter, SQLSetDescFields e SQLSetDescRec avranno esito negativo con SQLSTATE 07006 e il messaggio "violazione dell'attributo del tipo di dati (la versione di SQL Server per questa connessione non supporta  
  
## <a name="see-also"></a>Vedere anche  
 [Parametri con valori di tabella &#40;&#41;ODBC](table-valued-parameters-odbc.md)  
  
  
