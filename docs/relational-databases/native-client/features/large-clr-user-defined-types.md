---
title: Tipi definiti dall'utente CLR di grandi dimensioni | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.reviewer: ''
ms.prod: sql
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- large CLR user-defined types
ms.assetid: b65eb61d-ccf6-49c0-98e7-9a4ef4b2f790
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0176ba03151b084cb26eda03969b1e83afb1820d
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56020273"
---
# <a name="large-clr-user-defined-types"></a>Tipi CLR definiti dall'utente di grandi dimensioni
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  In SQL Server 2005 i tipi definiti dall'utente in CLR (Common Language Runtime) sono limitati a dimensioni di 8.000 byte. Questa restrizione è stata eliminata in [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] e versioni successive. In questa versione i tipi CLR definiti dall'utente vengono considerati simili ai tipi LOB. Tipi definiti dall'utente minori o uguali a 8.000 byte, pertanto, hanno lo stesso comportamento che in SQL Server 2005, ma sono supportati dati definiti dall'utente di dimensioni maggiori, che vengono indicate come illimitate ("unlimited").  
  
 Per altre informazioni, vedere [Large CLR User-Defined tipi &#40;OLE DB&#41; ](../../../relational-databases/native-client/ole-db/large-clr-user-defined-types-ole-db.md) e [Large CLR User-Defined tipi &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="use-cases"></a>Casi d'uso  
 Per ODBC, il supporto per i tipi definiti dall'utente di grandi dimensioni include la possibilità di inviare i valori di tali tipi in parti come parametri data-at-execution. Questa operazione viene eseguita dall'uso di SQLPutData.  
  
 Per OLE DB, il supporto per i tipi definiti dall'utente di grandi dimensioni include la possibilità di eseguire il flusso dei valori di tali tipi al e dal server usando l'associazione ISequentialStream.  
  
 Tipi definiti dall'utente minori o uguali a 8.000 byte hanno lo stesso comportamento che in SQL Server 2005. Per OLE DB, si può comunque trasmettere piccole tipi definiti dall'utente tramite il binding di ISequentialStream.  
  
 Il codice nativo dovrà talvolta riconoscere il contenuto dei tipi CLR definiti dall'utente, ma non dovrà creare istanze di oggetti gestiti. In tal caso, è possibile utilizzare serializzazione personalizzata per convertire i valori dei tipi definiti dall'utente nel server in un formato noto per i client.  
  
 Per le applicazioni che dispongono di codice di accesso ai dati, è possibile sfruttare il comportamento dei tipi CLR definiti dall'utente nel client recuperando tali tipi tramite API native e creandone istanze tramite l'interoperabilità C++ CLI in applicazioni in modalità mista.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità di SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
