---
title: sp_syscollector_update_collector_type (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_update_collector_type_TSQL
- sp_syscollector_update_collector_type
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_update_collector_type
- data collector [SQL Server], stored procedures
ms.assetid: 3c414dfd-d9ca-4320-81aa-949465b967bf
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9d3529d01966c7f9780183d663823d8f4033f47a
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58535783"
---
# <a name="spsyscollectorupdatecollectortype-transact-sql"></a>sp_syscollector_update_collector_type (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiorna un tipo agente di raccolta per un elemento della raccolta. Dopo che sono stati specificati il nome e il valore GUID di un tipo agente di raccolta, aggiorna la configurazione del tipo agente di raccolta, includendo il pacchetto di raccolta e di caricamento, lo schema dei parametri e lo schema del formattatore dei parametri.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_syscollector_update_collector_type [ @collector_type_uid = ] 'collector_type_uid' OUTPUT  
          , [ @name = ] 'name'  
          , [ @parameter_schema = ] 'parameter_schema'  
          , [ @collection_package_id = ] collection_package_id  
          , [ @upload_package_id = ] upload_package_id  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @collector_type_uid = ] 'collector_type_uid'` È il GUID per il tipo di agente di raccolta. *collector_type_uid* viene **uniqueidentifier**, e se è NULL verrà creato automaticamente e restituito come OUTPUT.  
  
`[ @name = ] 'name'` È il nome del tipo di agente di raccolta. *nome* viene **sysname** e deve essere specificato.  
  
`[ @parameter_schema = ] 'parameter_schema'` È lo schema XML per questo tipo di agente di raccolta. *parameter_schema* viene **xml** e può essere richiesto da determinati tipi agente di raccolta. Se non è obbligatorio, questo argomento può essere NULL.  
  
`[ @collection_package_id = ] collection_package_id` È un identificatore univoco locale che punta al [!INCLUDE[ssIS](../../includes/ssis-md.md)] pacchetto di raccolta utilizzato dal set di raccolta. *collection_package_id* viene **uniqueidentifier** ed è obbligatorio. Per ottenere il valore per *collection_package_id*, eseguire query sulla vista di sistema syscollector_collector_types nel database msdb.  
  
`[ @upload_package_id = ] upload_package_id` È un identificatore univoco locale che punta al [!INCLUDE[ssIS](../../includes/ssis-md.md)] Carica pacchetto utilizzato dal set di raccolta. *upload_package_id* viene **uniqueidentifier** ed è obbligatorio. Per ottenere il valore per *upload_package_id*, eseguire query sulla vista di sistema syscollector_collector_types nel database msdb.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="permissions"></a>Permissions  
 Richiede l'appartenenza al **dc_admin** (con autorizzazione EXECUTE) ruolo predefinito del database.  
  
## <a name="example"></a>Esempio  
 In questo esempio viene aggiornato il tipo agente di raccolta query T-SQL generico. Nell'esempio viene utilizzato lo schema predefinito per il tipo agente di raccolta query T-SQL generico.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collector_type  
@collector_type_uid = '302E93D1-3424-4BE7-AA8E-84813ECF2419',  
@name = 'Generic T-SQL Query Collector Type',  
@parameter_schema = '<?xml version="1.0" encoding="utf-8"?>  
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" targetNamespace="DataCollectorType">  
  <xs:element name="TSQLQueryCollector">  
<xs:complexType>  
  <xs:sequence>  
<xs:element name="Query" minOccurs="1" maxOccurs="unbounded">  
  <xs:complexType>  
<xs:sequence>  
  <xs:element name="Value" type="xs:string" />  
  <xs:element name="OutputTable" type="xs:string" />  
</xs:sequence>  
  </xs:complexType>  
</xs:element>  
<xs:element name="Databases" minOccurs="0" maxOccurs="1">  
  <xs:complexType>  
<xs:sequence>  
  <xs:element name="Database" minOccurs="0" maxOccurs="unbounded" type="xs:string" />  
</xs:sequence>  
<xs:attribute name="UseSystemDatabases" type="xs:boolean" use="optional" />  
<xs:attribute name="UseUserDatabases" type="xs:boolean" use="optional" />  
  </xs:complexType>  
</xs:element>  
  </xs:sequence>  
</xs:complexType>  
  </xs:element>  
</xs:schema>',  
@collection_package_id = '292B1476-0F46-4490-A9B7-6DB724DE3C0B',  
@upload_package_id = '6EB73801-39CF-489C-B682-497350C939F0';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Raccolta dati](../../relational-databases/data-collection/data-collection.md)  
  
  
