---
description: xml_schema_namespace
title: xml_schema_namespace (Transact-SQL)
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- xml_schema_namespace_TSQL
- xml_schema_namespace
dev_langs:
- TSQL
helpviewer_keywords:
- XML schema collections [SQL Server], reconstructing schemas
- xml_schema_namespace function
- reconstructing schemas
- schemas [SQL Server], XML
- schema collections [SQL Server], reconstructing schemas
ms.assetid: ee9873d8-dd3a-4bff-a10c-68bbadbdf1a6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c74b2b1f47c9e928d7c3028add043e539134828d
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "91112981"
---
# <a name="xml_schema_namespace"></a>xml_schema_namespace
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Ricostruisce tutti gli schemi o uno schema specifico nella raccolta di XML Schema specificata. Questa funzione restituisce un'istanza del tipo di dati **xml** .  
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```syntaxsql
xml_schema_namespace( Relational_schema , XML_schema_collection_name , [ Namespace ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argomenti
 *Relational_schema*  
 Nome dello schema relazionale. *Relational_schema* è **sysname**.  
  
 *XML_schema_collection_name*  
 Nome della raccolta di XML Schema da ricostruire. *XML_schema_collection_name* è **sysname**.  
  
 *Spazio dei nomi*  
 Spazio dei nomi URI di XML Schema che si desidera ricostruire. La lunghezza massima è 1000 caratteri. Se l'URI dello spazio dei nomi viene omesso, viene ricostruita l'intera raccolta di XML Schema. *Namespace* è **nvarchar(4000)** .  
  
## <a name="return-types"></a>Tipi restituiti  
 **xml**  
  
## <a name="remarks"></a>Osservazioni  
 Quando si importano i componenti di XML Schema nel database tramite [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md) o [ALTER XML SCHEMA COLLECTION](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md), vengono preservati aspetti dello schema usati per la convalida. Pertanto, lo schema ricostruito può non corrispondere al documento dello schema originale dal punto di vista lessicale. Più specificamente, vengono persi i commenti, gli spazi vuoti e le annotazioni, mentre le informazioni implicite sui tipi vengono rese esplicite. Ad esempio \<xs:element name="e1" /> diventa \<xs:element name="e1" type="xs:anyType"/>. Inoltre, non vengono mantenuti i prefissi degli spazi dei nomi.  
  
 Se si specifica un parametro relativo allo spazio dei nomi, il documento dello schema risultante conterrà le definizioni per tutti i componenti degli schemi in quello spazio dei nomi, anche se erano state aggiunte in passaggi DDL o documenti di schemi diversi, o in entrambi.  
  
 Non è possibile usare questa funzione per costruire documenti di XML Schema dalla raccolta di XML Schema **sys.sys**.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene recuperata la raccolta di XML Schema `ProductDescriptionSchemaCollection` dallo schema relazionale di produzione nel database `AdventureWorks`.  
  
```sql
USE AdventureWorks;  
GO  
SELECT xml_schema_namespace(N'production',N'ProductDescriptionSchemaCollection');  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare una raccolta di XML Schema archiviata](../../relational-databases/xml/view-a-stored-xml-schema-collection.md)   
 [Raccolte di XML Schema &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
