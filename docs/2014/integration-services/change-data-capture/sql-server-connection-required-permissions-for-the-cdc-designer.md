---
title: Autorizzazioni necessarie della connessione di SQL Server per la finestra di progettazione di CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 80334de2-17c1-43c9-951e-21a9f864e9cb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 567ee5d4c6f57d4b4eb08cbd4ecac7aef999aa55
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62835417"
---
# <a name="sql-server-connection-required-permissions-for-the-cdc-designer"></a>Autorizzazioni necessarie della connessione di SQL Server per la finestra di progettazione di CDC
  Per eseguire attività in CDC Designer Console è necessario specificare le informazioni di connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . In questo argomento vengono illustrate le informazioni che è possibile specificare nella finestra di dialogo **Connect to SQL Server** per l'impostazione della connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 La finestra di dialogo **Connect to SQL Server** viene visualizzata quando necessario, ad esempio quando le informazioni di connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non sono disponibili o quando le informazioni sono presenti, ma la connessione non dispone delle autorizzazioni necessarie.  
  
 Nella tabella seguente vengono descritte le diverse attività per le quali è necessario disporre di una connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e le autorizzazioni necessarie relative all'utente o all'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Attività|Autorizzazioni minime|  
|----------|-------------------------|  
|Visualizzare l'elenco di servizi e istanze di CDC utilizzando l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associata.|`db_datareader` per MSXDBCDC|  
|Avviare/arrestare l'istanza di CDC)|`db_datareader` e `db_datawriter` per MSXDBCDC|  
|Visualizzare lo stato dell'istanza di CDC.|`db_owner` per il database dell'istanza di CDC|  
|Creare un nuovo database dell'istanza di Oracle CDC.|`dbcreator` Ruolo predefinito del server|  
|Creare una nuova istanza di Oracle CDC.|`db_datareader` per MSXDBCDC<br /><br /> `db_owner` per il database CDC creato.|  
|Ottenere gli script di distribuzione.|`db_datareader` e `db_datawriter` per MSXDBCDC<br /><br /> `db_owner` per il database CDC correlato|  
|Modificare la configurazione e aggiungere/rimuovere istanze di acquisizione.|`db_datareader` e `db_datawriter` per MSXDBCDC<br /><br /> `db_owner` per il database CDC correlato|  
  
## <a name="see-also"></a>Vedere anche  
 [Accedere a CDC Designer Console](access-the-cdc-designer-console.md)   
 [Connessione di SQL Server per la creazione dell'istanza](sql-server-connection-for-instance-creation.md)  
  
  
