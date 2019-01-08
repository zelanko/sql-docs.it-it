---
title: Gestione connessione ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], ODBC
- ODBC connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], ODBC
ms.assetid: e8c77aa7-6772-485e-918e-cef9eeb18c58
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 57bd700e33836835218ee261a3f22211b9b4cb73
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52762437"
---
# <a name="odbc-connection-manager"></a>gestione connessione ODBC
  Una gestione connessione ODBC consente la connessione di un pacchetto a un'ampia gamma di sistemi di gestione di database in base alla specifica ODBC (Open Database Connectivity).  
  
 Quando si aggiunge una connessione ODBC a un pacchetto e impostare le proprietà di gestione connessione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una gestione connessione e aggiunge la gestione connessione per il `Connections` insieme del pacchetto. In fase di esecuzione la gestione connessione viene risolta in una connessione ODBC fisica.  
  
 La proprietà `ConnectionManagerType` della gestione connessione viene impostata su `ODBC`.  
  
 Per configurare la gestione connessione ODBC, procedere nel modo seguente:  
  
-   Specificare una stringa di connessione che fa riferimento al nome di un'origine dei dati utente o di sistema.  
  
-   Specificare il server a cui connettersi.  
  
-   Indicare se la connessione viene mantenuta in fase di esecuzione.  
  
## <a name="configuration-of-the-odbc-connection-manager"></a>Configurazione della gestione connessione ODBC  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:  
  
-   [Riferimento all'interfaccia utente di Gestione connessione ODBC](../odbc-connection-manager-ui-reference.md)  
  
 Per informazioni sulla configurazione di una gestione connessione a livello di programmazione, vedere l'articolo relativo a <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Aggiunta di connessioni a livello di programmazione](../building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Connessioni in Integration Services &#40;SSIS&#41;](integration-services-ssis-connections.md)  
  
  
