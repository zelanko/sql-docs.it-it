---
title: Salvataggio di un pacchetto a livello di programmazione | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- programmatically saving a package
- saving a package programmatically
ms.assetid: 4204f817-d5df-475a-9338-d7f01305d566
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3630bbebf5c86b0e839fe51735cba4fb71763b8a
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86922707"
---
# <a name="saving-a-package-programmatically"></a>Salvataggio di un pacchetto a livello di programmazione

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Dopo avere compilato un nuovo pacchetto a livello di programmazione, o dopo averne modificato uno esistente, si desidera in genere salvare le modifiche.  
  
 Tutti i metodi usati in questo argomento per salvare pacchetti richiedono un riferimento all'assembly **Microsoft.SqlServer.ManagedDTS**. Dopo aver aggiunto il riferimento in un nuovo progetto, importare lo spazio dei nomi <xref:Microsoft.SqlServer.Dts.Runtime> con un'istruzione **using** o **Imports**.  
  
## <a name="saving-a-package-programmatically"></a>Salvataggio di un pacchetto a livello di programmazione  
 Per salvare un pacchetto a livello di programmazione, chiamare uno dei metodi seguenti della classe [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] di <xref:Microsoft.SqlServer.Dts.Runtime.Application>:  
  
|Posizione di archiviazione|Metodo da chiamare|  
|----------------------|--------------------|  
|File|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToXml%2A>|  
|Archivio pacchetti SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServer%2A><br /><br /> o<br /><br /> <xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServerAs%2A>|  
  
> [!IMPORTANT]  
>  I metodi della classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> per l'utilizzo dell'archivio pacchetti SSIS supportano solo "." o il nome del server locale. Non è possibile utilizzare "(local)" o "localhost".  
  
## <a name="see-also"></a>Vedere anche  
 [Salvare i pacchetti](../../integration-services/save-packages.md)  
  
  
