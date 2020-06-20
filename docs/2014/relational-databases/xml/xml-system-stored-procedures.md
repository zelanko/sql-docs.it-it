---
title: Stored procedure XML di sistema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- system stored procedures [SQL Server], XML
- sp_xml_removedocument
- OPENXML statement, system stored procedures
- sp_xml_preparedocument
- XML [SQL Server], system stored procedures
ms.assetid: e60c7f85-6823-4d28-93d6-b053d08cc830
author: rothja
ms.author: jroth
ms.openlocfilehash: 2008294fe5bc532dfb6883656420b4189e4da7b0
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85046262"
---
# <a name="xml-system-stored-procedures"></a>Stored procedure XML di sistema
  In SQL Server sono disponibili le stored procedure di sistema seguenti, utilizzate insieme all'istruzione OPENXML:  
  
-   [sp_xml_preparedocument &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql)  
  
-   [sp_xml_removedocument &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql)  
  
 Per scrivere le query tramite l'istruzione OPENXML, è prima necessario creare una rappresentazione interna del documento XML chiamando la stored procedure **sp_xml_preparedocument**. La stored procedure restituisce un handle per la rappresentazione interna del documento XML. Tale handle viene quindi passato a OPENXML, che restituisce viste di set di righe del documento basate su query XPath. In particolare, vengono restituiti un modello di riga e uno o più modelli di colonna.  
  
> [!NOTE]  
>  L'handle del documento restituito dalla stored procedure **sp_xml_preparedocument** è valido per l'intera durata della sessione.  
  
 È possibile rimuovere la rappresentazione interna del documento XML dalla memoria chiamando la stored procedure di sistema **sp_xml_removedocument** .  
  
## <a name="see-also"></a>Vedere anche  
 [OPENXML &#40;Transact-SQL&#41;](/sql/t-sql/functions/openxml-transact-sql)   
 [OPENXML &#40;SQL Server&#41;](../xml/openxml-sql-server.md)  
  
  
