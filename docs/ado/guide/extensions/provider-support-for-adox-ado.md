---
title: Supporto del provider per ADOX (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADOX provider support [ADO]
ms.assetid: 64234ce5-dc46-4c8a-a316-61956b6b9abb
author: rothja
ms.author: jroth
ms.openlocfilehash: b9e0fa4184a9d86efcda9c2d67870df5f98ed664
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82748163"
---
# <a name="provider-support-for-adox-ado"></a>Supporto dei provider per ADOX (ADO)
Alcune funzionalità di ADOX non sono supportate, a seconda del provider di dati OLE DB. ADOX è completamente supportato con il [provider di OLE DB per Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md). Nelle tabelle seguenti sono elencate le funzionalità non supportate con il [provider di microsoft OLE DB per SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), il [provider di OLE DB Microsoft per ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)o il [provider Microsoft OLE DB per Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) . ADOX non è supportato da altri provider di OLE DB Microsoft.  
  
## <a name="microsoft-ole-db-provider-for-sql-server"></a>Provider Microsoft OLE DB per SQL Server  
  
|Oggetto o raccolta|Restrizione di utilizzo|  
|--------------------------|-----------------------|  
|Raccolta **Tables**|Le proprietà sono di lettura/scrittura prima della creazione dell'oggetto e di sola lettura quando fanno riferimento a un oggetto esistente.|  
|Raccolta **views**|Le **visualizzazioni** non sono supportate.|  
|Raccolta **Procedures**|I metodi **Append** ed **Delete** non sono supportati.|  
|Oggetto **procedure**|La proprietà **Command** non è supportata.|  
|Raccolta di **chiavi**|I metodi **Append** ed **Delete** non sono supportati.|  
|Raccolta **utenti**|**Utenti** non supportati.|  
|Raccolta di **gruppi**|I **gruppi** non sono supportati.|  
  
## <a name="microsoft-ole-db-provider-for-odbc"></a>Provider Microsoft OLE DB per ODBC  
  
|Oggetto o raccolta|Restrizione di utilizzo|  
|--------------------------|-----------------------|  
|Oggetto **Catalog**|Il metodo **create** non è supportato.|  
|Raccolta **Tables**|I metodi **Append** ed **Delete** non sono supportati. Le proprietà sono di lettura/scrittura prima della creazione dell'oggetto e di sola lettura quando fanno riferimento a un oggetto esistente.|  
|Raccolta **Procedures**|I metodi **Append** ed **Delete** non sono supportati.|  
|Oggetto **procedure**|La proprietà **Command** non è supportata.|  
|Raccolta **indexes**|I metodi **Append** ed **Delete** non sono supportati.|  
|Raccolta di **chiavi**|I metodi **Append** ed **Delete** non sono supportati.|  
|Raccolta **utenti**|**Utenti** non supportati.|  
|Raccolta di **gruppi**|I **gruppi** non sono supportati.|  
  
## <a name="microsoft-ole-db-provider-for-oracle"></a>Provider OLE DB per Oracle  
  
|Oggetto o raccolta|Restrizione di utilizzo|  
|--------------------------|-----------------------|  
|Oggetto **Catalog**|Il metodo **create** non è supportato.|  
|Raccolta **Tables**|I metodi **Append** ed **Delete** non sono supportati. Le proprietà sono di lettura/scrittura prima della creazione dell'oggetto e di sola lettura quando fanno riferimento a un oggetto esistente.|  
|Raccolta **views**|I metodi **Append** ed **Delete** non sono supportati.|  
|Oggetto **View**|La proprietà **Command** non è supportata.|  
|Oggetto **Procedures**|I metodi **Append** ed **Delete** non sono supportati.|  
|Oggetto **procedure**|La proprietà **Command** non è supportata.|  
|Raccolta **indexes**|I metodi **Append** ed **Delete** non sono supportati.|  
|Raccolta di **chiavi**|I metodi **Append** ed **Delete** non sono supportati.|  
|Raccolta **utenti**|**Utenti** non supportati.|  
|Raccolta di **gruppi**|I **gruppi** non sono supportati.|
