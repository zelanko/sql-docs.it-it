---
description: Advanced Connection Properties
title: Advanced Connection Properties | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4edfab68-7e68-45e8-a3f3-a0049ff7eb9e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fd7ed8863356ff3e6b67d456628bd3dbc1ab6a5b
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123744"
---
# <a name="advanced-connection-properties"></a>Advanced Connection Properties

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Utilizzare la finestra di dialogo **Advanced Connection Properties** per aggiungere ulteriori parametri di connessione alla stringa di connessione.  
  
 Può trattarsi di qualsiasi parametro di connessione ODBC supportato dall'istanza del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in uso.  
  
 I parametri aggiunti utilizzando la finestra di dialogo **Advanced Connection Properties** vengono aggiunti ai parametri selezionati nella finestra di dialogo **Connect to SQL Server** .  
  
 L'ultima istanza di ogni parametro specificato sostituisce eventuali istanze precedenti del parametro stesso. I parametri aggiunti utilizzando la finestra di dialogo **Advanced Connection Parameters** seguono e sostituiscono i parametri specificati nella finestra di dialogo **SQL Server Connection** . Ad esempio, se nella finestra di dialogo **Connessione SQL Server** si specifica SERVER1 come nome del server e la pagina **Parametri aggiuntivi per la connessione** contiene ;SERVER=SERVER2, la connessione viene stabilita con SERVER2.  
  
 I parametri aggiunti utilizzando la finestra di dialogo **Advanced Connection Properties** vengono passati come testo normale.  
  
> [!IMPORTANT]  
>  Non includere le credenziali di accesso nella finestra di dialogo **Advanced Connection Properties** , non verranno crittografate quando vengono passate in rete.  
  
## <a name="see-also"></a>Vedere anche  
 [Accedere a CDC Designer Console](../../integration-services/change-data-capture/access-the-cdc-designer-console.md)   
 [Connessione di SQL Server per la creazione dell'istanza](../../integration-services/change-data-capture/sql-server-connection-for-instance-creation.md)  
  
  
