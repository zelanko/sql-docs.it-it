---
title: SQLXML non è installato in SQL Server | Documenti di Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 3dbb4f65-41de-48b8-ad62-47c9d7932de3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8fe1d4b937e5972eb90e567ded91f7a23af577d0
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/22/2019
ms.locfileid: "66012157"
---
# <a name="sqlxml-is-not-installed-in-sql-server"></a>Installazione di SQLXML non inclusa in SQL Server
  Prima di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], SQLXML 4.0 veniva rilasciato con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e faceva parte dell'installazione predefinita di tutte le versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ad eccezione di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. A partire da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], la versione più recente di SQLXML (SQLXML 4.0 SP1) non è più inclusa in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per installare SQLXML 4.0 SP1 quando disponibile, scaricarlo dal [Install Location for SQLXML SP1](https://www.microsoft.com/download/details.aspx?id=16978).  
  
 Se per un'applicazione eseguita su [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è richiesto SQLXML 4.0 e nel computer non è presente [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], è necessario scaricare e installare SQLXML 4.0 SP1.  
  
## <a name="sqlxml-40-sp1-behavior-with-new-data-types-using-sqloledb-and-sql-server-native-client-ole-db-provider"></a>Comportamento di SQLXML 4.0 SP1 con i nuovi tipi di dati quando si utilizzano il provider OLE DB di SQL Server Native Client e SQLOLEDB  
 In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] vengono introdotti i tipi di dati seguenti che possono essere impiegati dagli sviluppatori che utilizzano SQLXML:  
  
-   `Date`  
  
-   `Time`  
  
-   `DateTime2`  
  
-   `DateTimeOffset`  
  
 Quando si utilizza SQLXML 4.0 SP1 con SQLOLEDB (da Windows Data Access Components, prima noto come Microsoft Data Access Components) o con il provider OLE DB di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], i nuovi tipi vengono visualizzati sotto forma di stringhe agli sviluppatori. I quattro nuovi tipi di dati vengono abilitati come tipi scalari predefiniti quando SQLXML 4.0 SP1 viene utilizzato con il provider OLE DB di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 11.0 Se non si scarica SQLXML 4.0 SP1, l'esecuzione del mapping di questi tipi ai tipi non stringa può causare il troncamento dei dati. Ad esempio, il mapping `DateTime2` al `xsd:date` determinerà dati troncati per il [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] `DateTime` precisione di 3,33 millisecondi.  
  
## <a name="see-also"></a>Vedere anche  
 [Concetti relativi alla programmazione SQLXML 4.0](sqlxml-4-0-programming-concepts.md)  
  
  
