---
title: sp_syscollector_create_collector_type (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_create_collector_type
- sp_syscollector_create_collector_type_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_create_collector_type
- data collector [SQL Server], stored procedures
ms.assetid: 568e9119-b9b0-4284-9cef-3878c691de5f
author: stevestein
ms.author: sstein
ms.openlocfilehash: bd8c82a401f78f4907bb891ede845017c00ac5ad
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68032629"
---
# <a name="sp_syscollector_create_collector_type-transact-sql"></a>sp_syscollector_create_collector_type (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un tipo di agente di raccolta per l'agente di raccolta dati. Un tipo di agente di raccolta è un wrapper [!INCLUDE[ssIS](../../includes/ssis-md.md)] logico intorno ai pacchetti che fornisce il meccanismo effettivo per raccogliere dati e caricarli nel data warehouse di gestione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_syscollector_create_collector_type   
    [ [@collector_type_uid = ] 'collector_type_uid' OUTPUT ]  
    , [ @name = ] 'name'  
    , [ [ @parameter_schema = ] 'parameter_schema' ]  
    , [ [ @parameter_formatter = ] 'parameter_formatter' ]  
    , [ @collection_package_id = ] 'collection_package_id'  
    , [ @upload_package_id = ] 'upload_package_id'  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @collector_type_uid = ] '*collector_type_uid*'  
 GUID del tipo di agente di raccolta. *collector_type_uid* è di tipo **uniqueidentifier** e se è null, verrà creata e restituita automaticamente come output.  
  
 [ @name = ] '*Name*'  
 Nome del tipo di agente di raccolta. *Name* è di **tipo sysname** e deve essere specificato.  
  
 [ @parameter_schema = ] '*parameter_schema*'  
 XML Schema per questo tipo di agente di raccolta. *parameter_schema* è di **XML** e il valore predefinito è null.  
  
 [ @parameter_formatter = ] '*parameter_formatter*'  
 Modello da utilizzare per trasformare l'XML per l'utilizzo nella pagina delle proprietà del set di raccolta. *parameter_formatter* è di **XML** e il valore predefinito è null.  
  
 [@collection_package_id = ] *collection_package_id*  
 È un identificatore univoco locale che punta al pacchetto di raccolta [!INCLUDE[ssIS](../../includes/ssis-md.md)] utilizzato dal set di raccolta. *collection_package_id* è **uniqueidentifier** ed è obbligatorio.  
  
 [@upload_package_id = ] *upload_package_id*  
 Identificatore univoco locale che punta al pacchetto di caricamento di [!INCLUDE[ssIS](../../includes/ssis-md.md)] utilizzato dal set di raccolta. *upload_package_id* è di tipo **uniqueidentifier** ed è obbligatorio.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="permissions"></a>Autorizzazioni  
 Per eseguire questa procedura, è richiesta l'appartenenza al ruolo predefinito del database dc_admin (con autorizzazione EXECUTE) .  
  
## <a name="example"></a>Esempio  
 Viene creato il tipo di agente di raccolta query T-SQL generico.  
  
```  
EXEC sp_syscollector_create_collector_type  
@collector_type_uid = '302E93D1-3424-4be7-AA8E-84813ECF2419',  
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
  
  
