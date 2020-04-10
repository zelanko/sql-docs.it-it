---
title: Esecuzione di transazioni con il driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: afbb776f-05dc-4e79-bb25-2c340483e401
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aa86cde4d8c7d0aa91b5864f5beb3317b91bf0ee
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923747"
---
# <a name="performing-transactions-with-the-jdbc-driver"></a>Esecuzione di transazioni con il driver JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  L'elaborazione delle transazioni è un requisito indispensabile di tutte le applicazioni che devono garantire la coerenza dei dati persistenti. Con [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] tale operazione può essere eseguita in modalità locale o distribuita. Le transazioni sono moduli di esecuzione atomici, consistenti, isolati e duraturi, provvisti cioè delle cosiddette proprietà ACID.  
  
 Negli argomenti di questa sezione viene descritto in che modo il driver JDBC supporta le transazioni e i livelli di isolamento, i punti di salvataggio delle transazioni e la trattenibilità dei set di risultati.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Informazioni sulle transazioni](../../connect/jdbc/understanding-transactions.md)|Fornisce una panoramica del modo in cui vengono utilizzate le transazioni con il driver JDBC.|  
|[Informazioni sulle transazioni XA](../../connect/jdbc/understanding-xa-transactions.md)|Fornisce una panoramica del modo in cui vengono utilizzate le transazioni XA con il driver JDBC.|  
|[Informazioni sui livelli di isolamento](../../connect/jdbc/understanding-isolation-levels.md)|Descrive i diversi livelli di isolamento supportati dal driver JDBC.|  
|[Uso dei punti di salvataggio](../../connect/jdbc/using-savepoints.md)|Descrive come utilizzare il driver JDBC con i punti di salvataggio delle transazioni.|  
|[Uso della trattenibilità](../../connect/jdbc/using-holdability.md)|Descrive come utilizzare il driver JDBC con la trattenibilità dei set di risultati.|  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica del driver JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
