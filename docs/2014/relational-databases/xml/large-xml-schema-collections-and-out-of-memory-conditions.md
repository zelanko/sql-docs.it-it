---
title: Raccolte di XML Schema di grandi dimensioni e condizioni di memoria insufficiente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- out-of-memory conditions
- XML schema collections [SQL Server], large
ms.assetid: 29b9d839-aaaf-48fb-be17-840c751f36f1
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b5c82509505cb0497ffd67aa490e9b7d5f9b2a25
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82702613"
---
# <a name="large-xml-schema-collections-and-out-of-memory-conditions"></a>Raccolte di XML Schema di grandi dimensioni e condizioni di memoria insufficiente
  Durante una chiamata alla funzione incorporata XML_SCHEMA_NAMESPACE() in una raccolta XML Schema di grandi dimensioni o durante il tentativo di eliminare queste ultime, potrebbe verificarsi una condizione di memoria insufficiente. Per risolvere questo problema, è possibile utilizzare le soluzioni seguenti:  
  
-   Quando il carico di lavoro del sistema è ridotto, è consigliabile utilizzare il comando DROP_XML_SCHEMA_COLLECTION. Se tale tentativo ha esito negativo, configurare il database in modalità utente singolo mediante l'istruzione ALTER DATABASE e provare ad eseguire di nuovo il comando DROP XML SCHEMA COLLECTION. Se la raccolta XML Schema è contenuta nel database **master**, **model**o **tempdb**, per attivare la modalità utente singolo è necessario riavviare il server.  
  
-   Quando si chiama la funzione XML_SCHEMA_NAMESPACE, è possibile provare a recuperare un singolo spazio dei nomi XML Schema ; provare a eseguire la chiamata quando diminuisce il carico di lavoro del sistema oppure provare ad eseguirla in modalità utente singolo.  
  
## <a name="see-also"></a>Vedere anche  
 [Requisiti e limitazioni per le raccolte di XML Schema nel server](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
