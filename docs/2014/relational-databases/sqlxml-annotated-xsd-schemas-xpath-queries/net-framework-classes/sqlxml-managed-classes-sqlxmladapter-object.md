---
title: Oggetto SqlXmlAdapter (classi gestite SQLXML) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- void Update(DataSet ds) method
- SqlXmlAdapter object
- void Fill(DataSet ds) method
- SQLXML Managed Classes, SqlXmlAdapter object
- Managed Classes [SQLXML], SqlXmlAdapter object
ms.assetid: 0a16eddf-fc26-4d92-82d4-359b5fb905d5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b339e67b07ddb4168f9922c22e620eb2fa10d85e
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/22/2019
ms.locfileid: "66014926"
---
# <a name="sqlxmladapter-object-sqlxml-managed-classes"></a>Oggetto SqlXmlAdapter (classi gestite SQLXML)
  Questo oggetto fornisce metodi che facilitano l'interazione con il set di dati in [!INCLUDE[msCoName](../../../includes/msconame-md.md)].NET Framework. Per un esempio funzionante, vedere [l'accesso a funzionalità SQLXML nell'ambiente .NET](accessing-sqlxml-functionality-in-the-net-environment.md).  
  
 L'oggetto SqlXmlAdapter supporta questi metodi:  
  
 void Fill (DataSet ds)  
 Inserisce nel set di dati di .NET Framework i dati XML recuperati da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 void Update (DataSet ds)  
 Applica aggiornamenti ai record in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dai dati del set di dati.  
  
 L'oggetto SqlXmlAdapter supporta questi costruttori:  
  
```  
public SqlXmlAdapter(SqlXmlCommand  cmd)   
  
public SqlXmlAdapter(  
                     string commandText,   
                     SqlXmlCommandType cmdType,   
                     string connectionString  
                      )   
  
public SqlXmlAdapter(  
                     Stream commandStream,   
                     SqlXmlCommandType cmdType,   
                     string connectionString  
                     )   
```  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto SqlXmlCommand &#40;classi gestite SQLXML&#41;](sqlxml-4-0-net-framework-support-managed-classes.md)   
 [Oggetto SqlXmlParameter &#40;classi gestite SQLXML&#41;](sqlxml-managed-classes-sqlxmlparameter-object.md)  
  
  
