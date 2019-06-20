---
title: 'Creazione di set di righe con ICommand:: Execute | Documenti di Microsoft'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
- Execute method
ms.assetid: 9b530b7d-8165-49d4-a978-5ced17c6705e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3e81f322bde3c4439b26acebb0ad24c925d583a0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63183676"
---
# <a name="creating-rowsets-with-icommandexecute"></a>Creazione di set di righe con ICommand::Execute
  Per i set di righe creati tramite il metodo **ICommand::Execute** le proprietà desiderate nel set di righe risultante possono determinare restrizioni per il testo del comando. Si tratta di un fattore particolarmente critico per i consumer che supportano testo del comando dinamico.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Impossibile utilizzare Native Client OLE DB provider [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursori per supportare i risultati di più set di righe generati da vari comandi. Se un consumer richiede un set di righe per cui è necessario il supporto del cursore [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si verifica un errore se il testo del comando genera più di un singolo set di righe come risultato. Per ulteriori informazioni, vedere [risultati più set di righe di generazione di comandi](../native-client-ole-db-commands/commands-generating-multiple-rowset-results.md).  
  
 Scorrevole [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client rowset OLE DB provider sono supportati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i cursori. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] impone limitazioni sui cursori che sono sensibili alle modifiche apportate dagli altri utenti del database. In particolare, le righe in alcuni cursori non possono essere ordinate e il tentativo di creare un set di righe tramite un comando che contiene una clausola SQL ORDER BY può non riuscire. Per altre informazioni, vedere [Set di righe e cursori SQL Server](rowsets-and-sql-server-cursors.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Set di righe](rowsets.md)  
  
  
