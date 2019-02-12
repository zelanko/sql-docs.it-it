---
title: Architettura della formattazione (SQLXML 4.0) XML sul lato Client e lato Server | Documenti di Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- providers [SQLXML], XML formatting architecture
- SQLOLEDB provider
- client-side XML formatting
- data providers [SQLXML], XML formatting architecture
- SQLNCLI, XML
- server-side XML formatting
- SQL Server Native Client, XML
- SQLXMLOLEDB Provider, XML formatting architecture
ms.assetid: 52440d9e-89fd-4c15-a008-a1ea99f41387
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 44e8d02cd90000a3a473a2e864345c483e5fda9d
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56028942"
---
# <a name="architecture-of-client-side-and-server-side-xml-formatting-sqlxml-40"></a>Architettura della formattazione XML sul lato client e sul lato server (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Nell'illustrazione seguente viene mostrata l'architettura della formattazione XML sul lato server.  
  
 ![Architettura della formattazione XML sul lato server. ](../../../relational-databases/sqlxml/formatting/media/serversidexml.gif "Formattazione sul lato server architettura di XML.")  
  
 In questo esempio il comando specificato sul client viene inviato al server. Il server produce un documento XML e lo restituisce al client. In questo caso, il server dispone di un'istanza di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Grazie alla formattazione XML sul lato server, è possibile utilizzare il provider SQLXMLOLEDB o il provider SQLOLEDB.  Il provider SQLXMLOLEDB utilizza Sqlxml4.dll che è incluso in SQLXML 4.0. Quando si utilizza il provider SQLOLEDB, per impostazione predefinita si ottiene la funzionalità SQLXML fornita dal file Sqlxmlx.dll incluso in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows o in Microsoft Data Access Components (MDAC) 2.6 o versione successiva. Per utilizzare Sqlxml4.dll con SQLOLEDB, è necessario impostare la proprietà SQLXML Version su "SQLXML.4.0" nell'oggetto SQLOLEDB connessione. In entrambi i casi, il server produce il documento XML e lo invia al client.  
  
> [!NOTE]  
>  Gli updategram e le query XPath vengono analizzati sul client. Per ottenere il modello XPath o la funzionalità degli updategram in SQLXML 4.0, utilizzare Sqlxml4.dll.  
  
 Nell'illustrazione seguente viene mostrata l'architettura della formattazione XML sul lato client.  
  
 ![Architettura della formattazione XML sul lato client. ](../../../relational-databases/sqlxml/formatting/media/clientsidexml.gif "Formattazione architettura di XML sul lato client.")  
  
 In questo esempio il client utilizza il provider SQLXMLOLEDB. Nella stringa di connessione, la proprietà Provider di dati deve essere impostata su SQLOLEDB. ovvero l'unico valore accettato in SQLXML 4.0. Il comando eseguito sul client viene inviato al server. Il set di righe generato nel server viene inviato al client. Sul client viene eseguita la formattazione del documento XML dal set di righe.  
  
 In SQLXML 4.0 è possibile utilizzare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) o il provider SQLOLEDB come provider di dati. È possibile accedere a qualsiasi origine dati. La trasformazione XML può essere applicata al client purché la query restituisca un singolo set di righe.  
  
  
