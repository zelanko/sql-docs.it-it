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
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 0f7642cd5f2245cbe5056ff09ec35477c0a6619c
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84920510"
---
# <a name="odbc-connection-manager"></a>gestione connessione ODBC
  Una gestione connessione ODBC consente la connessione di un pacchetto a un'ampia gamma di sistemi di gestione di database in base alla specifica ODBC (Open Database Connectivity).  
  
 Quando si aggiunge una connessione ODBC a un pacchetto e si impostano le proprietà della gestione connessione, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Crea una gestione connessione e la aggiunge alla `Connections` raccolta del pacchetto. In fase di esecuzione la gestione connessione viene risolta in una connessione ODBC fisica.  
  
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
  
  
