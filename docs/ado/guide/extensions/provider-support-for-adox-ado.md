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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e6f346779d3a4c8cb43e2b30347ebf6b198d9015
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63126874"
---
# <a name="provider-support-for-adox-ado"></a>Supporto dei provider per ADOX (ADO)
Alcune caratteristiche di ADOX non sono supportati, a seconda del provider di dati OLE DB. ADOX è completamente supportato con la [Provider OLE DB per Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md). Funzionalità non supportate con il [Provider Microsoft OLE DB per SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), il [Provider Microsoft OLE DB per ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md), o la [Provider Microsoft OLE DB per Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) sono elencate nelle tabelle seguenti. ADOX non è supportato da tutti gli altri provider Microsoft OLE DB.  
  
## <a name="microsoft-ole-db-provider-for-sql-server"></a>Provider Microsoft OLE DB per SQL Server  
  
|Oggetto o una raccolta|Restrizione di utilizzo|  
|--------------------------|-----------------------|  
|**Tabelle** raccolta|Proprietà sono di lettura/scrittura prima della creazione dell'oggetto e di sola lettura quando si fa riferimento un oggetto esistente.|  
|**Viste** raccolta|**Viste** non è supportato.|  
|**Le procedure** raccolta|Il **Append** e **eliminare** metodi non sono supportati.|  
|**Procedure** oggetto|Il **comando** proprietà non è supportata.|  
|**Le chiavi** raccolta|Il **Append** e **eliminare** metodi non sono supportati.|  
|**Gli utenti** raccolta|**Gli utenti** non è supportato.|  
|**Gruppi** raccolta|**Gruppi** non è supportato.|  
  
## <a name="microsoft-ole-db-provider-for-odbc"></a>Provider Microsoft OLE DB per ODBC  
  
|Oggetto o una raccolta|Restrizione di utilizzo|  
|--------------------------|-----------------------|  
|**Catalogo** oggetto|Il **Create** metodo non è supportato.|  
|**Tabelle** raccolta|Il **Append** e **eliminare** metodi non sono supportati. Proprietà sono di lettura/scrittura prima della creazione dell'oggetto e di sola lettura quando si fa riferimento un oggetto esistente.|  
|**Le procedure** raccolta|Il **Append** e **eliminare** metodi non sono supportati.|  
|**Procedure** oggetto|Il **comando** proprietà non è supportata.|  
|**Gli indici** raccolta|Il **Append** e **eliminare** metodi non sono supportati.|  
|**Le chiavi** raccolta|Il **Append** e **eliminare** metodi non sono supportati.|  
|**Gli utenti** raccolta|**Gli utenti** non è supportato.|  
|**Gruppi** raccolta|**Gruppi** non è supportato.|  
  
## <a name="microsoft-ole-db-provider-for-oracle"></a>Provider OLE DB per Oracle  
  
|Oggetto o una raccolta|Restrizione di utilizzo|  
|--------------------------|-----------------------|  
|**Catalogo** oggetto|Il **Create** metodo non è supportato.|  
|**Tabelle** raccolta|Il **Append** e **eliminare** metodi non sono supportati. Proprietà sono di lettura/scrittura prima della creazione dell'oggetto e di sola lettura quando si fa riferimento un oggetto esistente.|  
|**Viste** raccolta|Il **Append** e **eliminare** metodi non sono supportati.|  
|**Visualizzazione** oggetto|Il **comando** proprietà non è supportata.|  
|**Le procedure** oggetto|Il **Append** e **eliminare** metodi non sono supportati.|  
|**Procedure** oggetto|Il **comando** proprietà non è supportata.|  
|**Gli indici** raccolta|Il **Append** e **eliminare** metodi non sono supportati.|  
|**Le chiavi** raccolta|Il **Append** e **eliminare** metodi non sono supportati.|  
|**Gli utenti** raccolta|**Gli utenti** non è supportato.|  
|**Gruppi** raccolta|**Gruppi** non è supportato.|
