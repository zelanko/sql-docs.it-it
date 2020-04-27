---
title: ICommandWithParameters | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 66644c70-def7-46d8-8c47-b883292a0288
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ea85e526d99e586c2534eee8ab83c6ddc66939db
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62643257"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
  I miglioramenti apportati al motore di database a partire da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] consentono a ICommandWithParameters::GetParameterInfo di ottenere descrizioni più accurate dei risultati previsti. È possibile che questi risultati più accurati differiscano dai valori restituiti da CommandWithParameters::GetParameterInfo nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Metadata Discovery](../native-client/features/metadata-discovery.md).  
  
 A partire da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], inoltre, quando si chiama ICommandWithParameters::SetParameterInfo, il valore passato al parametro *pwszName* deve essere un identificatore valido. Per altre informazioni, vedere [Identificatori del database](../databases/database-identifiers.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Interfacce &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
