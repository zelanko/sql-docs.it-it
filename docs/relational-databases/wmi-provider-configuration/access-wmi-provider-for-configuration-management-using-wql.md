---
title: Utilizzare WQL per accedere al provider WMI
description: Utilizzare questo esempio per vedere come eseguire Strumentazione gestione Windows le istruzioni del linguaggio di query per il provider WMI per la gestione dei computer in SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Configuration Management, WQL
ms.assetid: 26499530-d93b-452b-bbe4-217ef1d11e68
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7efe4f3f8456dc68171b804d7afd28f565a4fbe2
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85888246"
---
# <a name="access-wmi-provider-for-configuration-management-using-wql"></a>Accedere al provider WMI per la gestione della configurazione tramite WQL
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  In questa sezione viene illustrato come eseguire le istruzioni WQL ([!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Management Instrumentation Query Language) sul provider WMI per Gestione computer.  
  
 Nell'esempio viene utilizzato un editor WQL, WBEMtest.exe, per eseguire query WQL sul provider WMI per enumerare i servizi, i protocolli di rete e gli alias di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="querying-services-using-wbemtest"></a>Esecuzione di query sui servizi mediante WBEMtest  
  
1.  Dal menu **Start** fare clic su **Esegui**, quindi immettere **WBEMTest**.  
  
2.  Viene visualizzata la finestra di dialogo WBEMtest.exe. Fare clic su **Connetti**.  
  
3.  Nel primo campo di testo digitare lo spazio dei nomi del provider WMI per Gestione computer: root\Microsoft\SqlServer\ComputerManagement11. Fare clic su **Connetti**.  
  
4.  Fare clic su **Query**. Digitare una query che restituisca i servizi correnti in esecuzione nel computer locale: **Select \* from SqlService.** Fare clic su **Apply**.  
  
5.  Perfezionare ulteriormente la query aggiungendo **where ServiceName = "MSSQLSERVER"**.  
  
  
