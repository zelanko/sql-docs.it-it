---
title: La memorizzazione nella cache modelli XSL e schemi (SQLXML 4.0) | Documenti di Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, caching
- cache [SQLXML]
- memory [SQLXML]
ms.assetid: 80b4fa79-243f-442c-9f22-74ad66186501
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ab740322ff0cf8847e12905cd0545667e7ae6f9b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001341"
---
# <a name="caching-templates-xsl-and-schemas-sqlxml-40"></a>Memorizzazione nella cache di modelli, file XSL e schemi (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Per migliorare le prestazioni,  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 supporta la memorizzazione di modelli, file XSL e schemi nella cache.  
  
 Tutti gli schemi, modelli e i file XSL (ad eccezione dei file da un https:// o ftp: / / percorso) vengono memorizzati nella cache. I file memorizzati nella cache restano in memoria mentre il processo è in esecuzione. Al termine del processo, il contenuto della cache va perso. Di conseguenza, se si esegue un processo per query, i vantaggi della memorizzazione nella cache potrebbero essere irrilevanti.  
  
 Negli argomenti di questa sezione vengono fornite ulteriori informazioni sulla memorizzazione nella cache.  
  
## <a name="in-this-section"></a>In questa sezione  
 [La cache dei modelli &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/template-caching-sqlxml-4-0.md)  
 Viene illustrata e quindi fornita una chiave del Registro di sistema per la memorizzazione nella cache dei modelli.  
  
 [La memorizzazione nella cache di XSL &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/xsl-caching-sqlxml-4-0.md)  
 Viene illustrata e quindi fornita una chiave del Registro di sistema per la memorizzazione nella cache dei file XSL.  
  
 [La cache dello schema &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/schema-caching-sqlxml-4-0.md)  
 Vengono illustrati i problemi dell'installazione affiancata di SQLXML relativi alla memorizzazione nella cache degli schemi e vengono fornite chiavi del Registro di sistema per la memorizzazione nella cache degli schemi.  
  
  
