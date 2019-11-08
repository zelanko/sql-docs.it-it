---
title: 'Creazione di set di righe con ICommand:: Execute | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 72b86e8642fd3af67cf6ca2952ae672914a71c1d
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73789006"
---
# <a name="creating-rowsets-with-icommandexecute"></a>Creazione di set di righe con ICommand::Execute
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Per i set di righe creati tramite il metodo **ICommand::Execute** le proprietà desiderate nel set di righe risultante possono determinare restrizioni per il testo del comando. Si tratta di un fattore particolarmente critico per i consumer che supportano testo del comando dinamico.  
  
 Il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client non è in grado di utilizzare i cursori [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per supportare i risultati di più set di righe generati da molti comandi. Se un consumer richiede un set di righe per cui è necessario il supporto del cursore [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si verifica un errore se il testo del comando genera più di un singolo set di righe come risultato. Per ulteriori informazioni, vedere [comandi che generano risultati con più set di righe](../../relational-databases/native-client-ole-db-commands/commands-generating-multiple-rowset-results.md).  
  
 I set di righe del provider OLE DB di Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono supportati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursori. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] impone limitazioni sui cursori che sono sensibili alle modifiche apportate dagli altri utenti del database. In particolare, le righe in alcuni cursori non possono essere ordinate e il tentativo di creare un set di righe tramite un comando che contiene una clausola SQL ORDER BY può non riuscire. Per altre informazioni, vedere [Set di righe e cursori SQL Server](../../relational-databases/native-client-ole-db-rowsets/rowsets-and-sql-server-cursors.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Set di righe](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
